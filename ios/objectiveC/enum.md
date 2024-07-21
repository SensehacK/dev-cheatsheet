
## [Swift Equivalent](ios/swift/enum.md)

## Syntax

```objc
typedef NS_ENUM(NSInteger, PPAsset) {
    PPAssetG6Video = 0,
    PPAssetG7Video = 0,
};
```

Funny enough `ObjectiveC` kinda truncates its enum name `PPAsset` and you can directly access it 

```swift
let assetClass: PPAsset = .G6Video
```

Which is odd to begin with.


Another example

```objc
typedef NS_ENUM(NSInteger, AppStatus) {
    AppStatusCreated = 0,
    AppStatusInitializing,
    AppStatusInitialized,
    AppStatusReady,
    AppStatusPlaying,
    AppStatusPaused,
    AppStatusStopped,
    AppStatusCompleted,
    AppStatusError
};
```