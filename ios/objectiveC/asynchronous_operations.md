# Asynchronous Operations


## Code

Objective C - call present with completion Handler.
```objC
- (void)presentWithCompletion:(void (^)(BOOL success))completion;
```

Swift has two ways to do this async operation
```swift
func present(completion: ((Bool) -> Void)? = nil)

func present() async -> Bool
```

## Reference

[apple dev | calling objC api async](https://developer.apple.com/documentation/swift/calling-objective-c-apis-asynchronously)