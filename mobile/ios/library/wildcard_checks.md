# Wildcard checks


## Check OS version

```swift

guard #available(iOS 14, *) else {
    print("Returning if iOS 13 or lower")
    return
}

print("This code only runs on iOS 14 and up")

```

[@available / available](https://www.avanderlee.com/swift/available-deprecated-renamed/)

[NSH](https://nshipster.com/available/)


## Check Library support

Checking if specific library is supported on the OS running the code or framework right now.
```swift
#if canImport(UIKit)
// iOS, tvOS, and watchOS – use UIColor
import UIKit
print("This code only runs if UIKit is supported on the device OS.")

#elseif canImport(AppKit)
// macOS – use NSColor
#else
// all other platforms – use a custom color object
#endif
```
[canImport HWS](https://www.hackingwithswift.com/example-code/language/how-to-check-whether-a-module-is-available-using-canimport)