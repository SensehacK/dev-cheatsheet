


## Code

```swift
var body: some View {

        VideoPlayer(player: AVPlayer(url:  URL(string: "http://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4")!))
            .frame(height: 400)
    }

```



## HIG

[apple dev | HIG | playing video](https://developer.apple.com/design/human-interface-guidelines/playing-video/)



## Errors


### playback error

Both of these were solved by switching from local to remote URL instantiation 
One is with normal URL and other is with Bundle.main.path url scheme. So depending on whether you're showing a video locally or remote you can work around these errors.


Local Video playback with `.mp4` or `.avi` files

```log
PVC/0-0 Received playback error: [Error Domain=AVFoundationErrorDomain Code=-11800 "The operation could not be completed" UserInfo={NSLocalizedFailureReason=An unknown error occurred (-17913), NSLocalizedDescription=The operation could not be completed, NSUnderlyingError=0x600000d0f810 {Error Domain=NSOSStatusErrorDomain Code=-17913 "(null)"}}]
```

```log
Error Domain=AVFoundationErrorDomain Code=-11850 "Operation Stopped" UserInfo={NSLocalizedFailureReason=The server is not correctly configured., NSLocalizedDescription=Operation Stopped, NSUnderlyingError=0x301d51800 {Error Domain=NSOSStatusErrorDomain Code=-12939 "(null)"}}]

```

