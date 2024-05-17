

## Debugging

Enable SSL proxying for specific URLs or wildcards if needed.


## Process

Charles generates a `.pem` file - Privacy Enhanced Mail (PEM) or `Base64 encoded certificate` as per Charles dialog box.
How `.pem` file differs from regular old OpenSSL key file - good thread to read [here](https://serverfault.com/questions/9708/what-is-a-pem-file-and-how-does-it-differ-from-other-openssl-generated-key-file)

```pem
-----BEGIN CERTIFICATE-----
MIIFVjCCBD6gAwIBAgIGAYlG5S1aMA0GCSqGSIb3DQEBCwUAMIGvMUAwPgYDVQQDDDdDaGFybGVz+VY=
-----END CERTIFICATE-----
```



Generating one is easy while using fastlane tool on macOS
[docs fastlane | pem](https://docs.fastlane.tools/actions/pem/)


## Generate Certificate

Go to `Charles` -> Help -> SSL Proxying -> Save Charles Root Certificate. 
You can save it as `.pem` Base 64 encoded certificate or 
`.cer` Binary Certificate



## tvOS

### Prerequisites 

If you want to configure for a physical tvOS apple tv 4K, you need few things to set it up.

- [Apple Configurator | app store](https://apps.apple.com/us/app/apple-configurator/id1037126344)
- [Charles Proxy 5.xx Beta](https://www.charlesproxy.com/beta/download.do)
- Apple TV 4K
- Same Wifi network with manual DHCP address reservation
- [node package manager](../tools/terminal/node#Node%20Version%20Manager)

### Steps

- create charles proxy from Menu -> Help -> SSL Proxying -> Save Charles Root Certificate... ” save it as `.cer` Binary Certificate `downloadedProfile.cer`
- Apple configurator -> File -> New Profile -> Name the profile "customTVOS_proxy" -> Select "Wifi", click "Configure"
- Fill your usual Wifi SSID (name: WifiName) & make sure `Proxy Setup` is selected to manual with provided `ProxyMan` Server and Port address eg. `10.0.0.22:9090`
- select “Certificates” → Click “Configure” → upload the `downloadedProfile.cer` file that you previously downloaded & renamed.
- save the profile `tvOSProxyProfile.mobileconfig` at accessible location & open a terminal at that `$pwd`
- Run a temporary [http server](../tools/server/http-server#Node) using node
- Make sure appleTV is on the same Wifi network 2.4 or 5Ghz and open Settings -> General -> Privacy & Security -> Share Apple TV Analytics. Press apple tv remote physical button `Play/Pause` new window will appear.
- Select `Add Profile`, add the mac http server ip address with port and local file complete path. eg: `http://10.0.0.22:8033/tvOSProxyProfile.mobileconfig` (easier to copy paste from mac shared clipboard to iPhone + tv remote Input prompt)
- Select "Install", few times and then we need to trust the certificate by heading over to Settings -> General ->   About ->   Certificate Trust Settings ->   Click on Proxy Profile ->   “Continue”.
- You may need to reenter your WiFi credentials again since for me it got disconnected once with tvOS 17.0 - apple TV 4K 2023.

Now you can see the logs of Apple tv 4K on Charles Proxy. I believe similar steps could be performed for [proxyman](proxyman.md)

##  Troubleshooting

### My internet connection doesn't work

Probably your Charles proxy server is being deallocated from the memory by OS schedulers. Check `Task Manager | Activity Monitor` just to see if the app is still consuming and listening for network events properly.

### Charles Profile doesn't download certificate `.pem` file

For me reinstalling the app and restarting the iPhone usually helps.
But to be extra cautious, check whether you have added `0.0.0.0/0` to the 
`Proxy > Access Control Settings` to give access to all the devices trying to route their proxy network traffic and give all iPv4 range table access to be allowed by default. It makes you avoid that pesky `Allow | Deny` confirmation dialogue box for the `Access Control Settings`
Also double check `Allow List` in Tools Menu is being enabled, disable that option if you don't want a whitelisted option for specific domains.


### Charles Profile doesn't show up on iOS Settings App
It is likely that your default browser is not `Safari` Apple kinda makes it PITA to always use their proprietary browser in order to do configuration profiles or certificates installs. I was using Firefox on iOS (Internal engine is still safari WebView WebKit Engine) with default browser selected as well since `Deeplinks` usually don't work on non default browser sometimes. But opening it on Safari with website `http://chls.pro/ssl` worked for me this time.


### Network requests shows `unknown` data

You need to go to Settings -> General -> About -> Certificate Trust Settings and toggle `Enable Full Trust for Root Certificates`

### Can no longer browse Internet without Charles

[charles proxy FAQ steps](https://www.charlesproxy.com/documentation/faqs/can-no-longer-browse-without-charles-running/)

### video playback buffering

```sh
DelioPlayer Media Failed. Description:1012.10 (Fairplay DRM):`The DRM delegate failed to acquire a license. (Delio)` Context: `(DelioPlayer) DRM Error` Delio Error Info 9004: `DelioError code:couldNotAcquireLicense.(9004)
assetURL:[http://ccr.linear-tve-ashburn-](http://ccr.linear-tve-sa-vss.top.sa.net/v1/frag/bmff/enc/cbcs/t/.m3u8?sz=urn:scte:224:audience:Zip:21412)


errorDescription" : "1001.2 (General Errors):`An unspecified network error occurred.` Context: `(DelioPlayer) Delio Error` Delio Error Info 4003: `DelioError code:playlistDeliveryUnableToDeliverPlaylist.
```

Turns out de-provisioning the security DRM client on the physical device solved this issue. Logging out and back works.

## Resources

[Kodeco | charles-proxy-tutorial-for-ios](https://www.kodeco.com/21931256-charles-proxy-tutorial-for-ios)


[Charles Proxy blocking SSL traffic on Android](https://stackoverflow.com/questions/53197681/charles-proxy-blocking-ssl-traffic-on-android)

