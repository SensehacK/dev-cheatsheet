
## Code

```swift
guard #available(iOS 14, *) else {
    print("Returning if iOS 13 or lower")
    return
}

print("This code only runs on iOS 14 and up")

if #available(iOS 15, *) { }
```

[avanderlee | @available / available](https://www.avanderlee.com/swift/available-deprecated-renamed/)

```swift
@available(iOS 13.0, macOS 10.15, *)
public class AsyncNetwork { }
```

[NSH | available](https://nshipster.com/available/)

[sarunw | how-to-handle-api-changes-with-@available](https://sarunw.com/posts/how-to-handle-api-changes-with-@available/)


## `@available` vs `#available`

`#available` is a tool for **API consumer**. 
checking for the availability

`@available` is a tool for **API creator**.
specify availability


## Conditional directive

`hasAttribute(AttributeName)`

```swift
#if hasAttribute(preconcurrency)
@preconcurrency
#endif
protocol P: Sendable { func f()  func g() }
```

`canImport(OSLibrary)` further explained in [check Library](wildcard_checks.md#check%20Library)

```swift
#if canImport(UIKit)
import UIKit
#endif
```

[sarunw | conditional compilation](https://sarunw.com/posts/conditional-compilation-for-attributes/)


