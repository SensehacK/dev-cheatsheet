
## Errors

### iOS 17


When failing drm delegate key request, prior to iOS 17, it used to automatically call `.failed()`

`keyRequest.processContentKeyResponseError` used to call `.failed()` inside it but somehow something changed on the iOS 17 side of things.

> b/c it was passed through `keyRequest.processContentKeyResponseError(helioError)` but was broken inside of iOS 17

Git diff

```swift
let mError = MError(code: .drmDelegateUnavailable, assetURL: assetURL)

// vs
self.failed(withError: mError)
keyRequest.processContentKeyResponseError(mError)
```

[no change documentation mentioned](<https://developer.apple.com/documentation/avfoundation/avcontentkeyrequest/processcontentkeyresponseerror(_:)#parameters>)

