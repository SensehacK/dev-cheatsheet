
## Syntax

Anything defined in `.h` header files are public by default.

```objc
/// CVideoEvent.h / m
@implementation CVideoEvent
NSString* const PLAY_STATE_CHANGED = @"PlayStateChanged";


/// CInternalVideoEvent.h / m
@implementation CInternalVideoEvent
NSString* const INTERNAL_PLAY_STATE_CHANGED = @"InternalPlayStateChanged";
```

Both are publicly available since there’s no such thing as “internal” where it’s scoped to only the current module


## [Swift Equivalent of access_control](ios/swift/access_control.md)