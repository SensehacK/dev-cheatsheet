
## PassThrough Subject

```swift
private let quotePub = PassthroughSubject<String, Never>()

```

## Behavior Subject

```swift
public class Custom { } // Model
let customContext = BehaviorSubject<Custom>(value: Custom())
```