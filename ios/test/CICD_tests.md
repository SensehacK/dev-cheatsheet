# CI/CD Tests


## Uncertainty build machine state

This was a great callout by my mentor around having explicit coupling of URL for test purposes.

```swift
let testURL = URL(string: "https://devstreaming-cdn.apple.com/videos/streaming/examples/adv_dv_atmos/main.m3u8")!
```

One thing I will call out here is you are relying on network to run these tests since this URL points to an actual HTTP remote URL.

This can add uncertainty in the future if the network gets disconnected from the build machine.

It's not something we need to change right now but I wanted to call it out as a potential problem in the future.

Another way around this might be to have an interface for `TrackOrchestrator` so you can Mock that directly without needing an AVPlayer instance.
