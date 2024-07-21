


## Extension


```swift
public extension Result {
    var isSuccess: Bool {
        if case .success = self {
            return true
        } else {
            return false
        }
    }
    var isError: Bool { !isSuccess }
}
```
