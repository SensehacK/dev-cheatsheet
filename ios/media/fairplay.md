

## Desc

FairPlay Streaming is a DRM (Digital Right Management) technology used to secure streaming media delivery to devices through the HTTP Live Streaming (HLS) protocol. Using FairPlay Streaming (FPS) technology, content providers can encrypt content, securely exchange keys, and protect playback on iOS, iPadOS, watchOS 7, tvOS, and macOS.


## Terms

IV - initialization vector
CDN - Content delivery network
SPC - Server Playback Context
CKC - content key context
KSM - Key Security Module

## Flow


[Copied from Bitmovin documentation](https://developer.bitmovin.com/playback/docs/how-does-fairplay-work#introduction)
### How does it work?

There are four components involved in decrypting FPS content:

- Apple Device (Such as an iPhone or iPad)
    - Target Application (Either a native app or a web app accessed via Safari)
    - Operating System (OS) (IOS, iPad OS, tvOS, macOS, etc.)
- DRM Key Server (Like BuyDRM or DRMToday)
    - Key Security Module (FPS KSM)
- Content Provider Server (Your key database)

### How do those elements interact to deliver secure content?

Below is an example workflow on how the Apple device, altogether with the Bitmovin Player and the DRM Key server and Content Provider server work together. Also, the main bullets show how the Bitmovin iOS SDK would handle those steps (based on this guide that is based on this Sample Application)

![](https://files.readme.io/2115959-FPS.png)

1. The Target Application does request the manifest URL (m3u8)

- In this first portion, we define:
    - The Target Application does request the manifest URL (m3u8)
        - fairplayStreamUrl - The target FPS-protected m3u8 playlist
        - certificateUrl - The URL to the FairPlay Streaming certificate of the license server. You need to previously process and generate this
        - Certificate from the Apple Developer Portal.
        - licenseUrl - The URL to the license server.

```swift
guard let fairplayStreamUrl = URL(string: "https://easeltvinternal.origin.mediaservices.windows.net/5cd4d1e2-a5c3-4223-862d-cfad90074e09/ETV_BIG_BUCK_BUNNY_1_FEATURE.ism/manifest(format=m3u8-aapl)"),
  let certificateUrl = URL(string: "http://demo.suggestedtvconfig.co.uk/bitdash/fairplay.cer"),
  let licenseUrl = URL(string: "https://easeltvinternal.keydelivery.mediaservices.windows.net/FairPlay/?KID=bb216c0f-c8f7-40b7-84da-8a7525f56635") else {
	print("Please specify the needed resources marked with TODO in ViewController.swift file.")
	return
}

let fpsConfig = FairplayConfig(license: licenseUrl, certificateURL: certificateUrl)
...
let sourceConfig = SourceConfig(url: fairplayStreamUrl, type: .hls)        
sourceConfig.drmConfig = fpsConfig
player.load(sourceConfig: sourceConfig)
```

1. The CDN responds with an FPS-protected m3u8 playlist
2. **The Target Application receives the manifest with FPS Signaling, checks it, and identifies it accordingly via the EXT-X-KEY tag with METHOD=SAMPLE-AES and KEYFORMAT="com.apple.streamingkeydelivery”; then, it notifies the OS to play FPS content, triggering subsequent actions**.
3. **The Target Application creates a key request and sends it back to the OS for encryption. This key request includes the content ID and an SPC (Server Playback Context) message.**

- The bellow code prepares the key request message with all the customer information the DRM server may need. This varies from the DRM server.

```swift
let fpsConfig = FairplayConfiguration(license: licenseUrl, certificateURL: certificateUrl)
let userData = "{\"userId\":\"YOURUSERID\", \"sessionId\":\"YOURSESSIONID\", \"merchant\":\"YOURMERCHANTSTRING\"}"
let data = (userData).data(using: String.Encoding.utf8)
let base64 = data!.base64EncodedString(options: NSData.Base64EncodingOptions(rawValue: 0))
fpsConfig.licenseRequestHeaders = ["x-dt-custom-data": base64]
fpsConfig.prepareContentId = { (contentId: String) -> String in
    let pattern="skd://drmtoday?"
    //let contentId = contentId.substring(from: pattern.endIndex)
    let contentId = String(contentId[pattern.endIndex...])
    print("contentId: \(contentId)")
    return contentId
}
fpsConfig.prepareMessage = { (data: Data, contentId: String) -> Data in
    let base64String = data.base64EncodedString()
    let uriEncodedMessage = base64String.addingPercentEncoding(withAllowedCharacters: CharacterSet.alphanumerics)!
    let message = "spc=\(uriEncodedMessage)&\(contentId)"
    print("message: \(message.data(using: String.Encoding.utf8)!)")
    return message.data(using: String.Encoding.utf8)!
}
```

1. **The OS sends an encrypted SPC to the Target Application.**
2. **The Target App sends this SPC encrypted message to the DRM key server**
3. The DRM key server uses the content ID to fetch the appropriate Key and initialization vector.
4. The Content Provider Server opens the SPC to extract the session key, the anti-replay seed, the integrity information, and the authentication materials. Additionally, the SPC includes a secured version of the content ID provided by the application for best practice server verification.
5. The DRM key server wraps the content key and the initialization vector according to the FPS specification. The integrity verification is optional, but it is part of the best practice requirements.
6. The DRM key server creates a content key context (CKC) in response to the application that contains the content key and the initialization vector.
7. **The client application then provides CKC to OS to request a play context.**

Above, in **bold**, are all the steps that the Bitmovin native or Web SDK takes care of for you. Also, keep in mind that in Mac OS and iOS Safari, the Content Decryption Module (CDM) and Encrypted Media Extension (EME) standards built into the Safari browser are used instead of the implementation in the client app.



## Debugging 


[apple docs | debugging fairplay](https://developer.apple.com/library/archive/technotes/tn2454/_index.html)

## Errors


### FairPlay Streaming is not supported on simulators

You need to disable fairplay streaming on simulators to run it appropriately.

```sh
*** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '*** -[AVContentKeySession initWithKeySystem:storageDirectoryAtURL:legacyWebKitCompatibilityMode:] FairPlay Streaming is not supported on simulators'
```


## Reverse Engineer apple DRM

[fairplay apple obfuscation](https://nicolo.dev/en/blog/fairplay-apple-obfuscation/)

[removing apple drm via CLI](https://mobsecguys.medium.com/removing-apple-drm-via-cli-f5c0d75ba6eb)

[decrypt fairplay on iOS 13 lower | github project](https://github.com/DerekSelander/yacd)

[ycombinator threads around decryption fairplay](https://news.ycombinator.com/item?id=37307653)

[Not screen recording | cydia tweak | github](https://github.com/opa334/opa334.github.io)


## References

DRM is pretty poorly documented, at least Apple's Fairplay solution. 
this article is somewhat helpful
[Apple DRM how does it work](https://ottverse.com/apple-fairplay-streaming-drm-how-does-it-work/)

[Playing Encrypted HLS content on iOS using swift](https://assist-software.net/snippets/how-play-encrypted-http-live-streams-offline-avfoundation-ios-using-swift-4)

[Wiki | FairPlay](https://en.wikipedia.org/wiki/FairPlay)