# Wildcard checks


## Check OS version

```swift

guard #available(iOS 14, *) else {
    print("Returning if iOS 13 or lower")
    return
}

print("This code only runs on iOS 14 and up")

if #available(iOS 15, *) { }
```

[@available / available](https://www.avanderlee.com/swift/available-deprecated-renamed/)

```swift
@available(iOS 13.0, macOS 10.15, *)
public class AsyncNetwork { }
```

[NSH](https://nshipster.com/available/)

[sarunw | how-to-handle-api-changes-with-@available](https://sarunw.com/posts/how-to-handle-api-changes-with-@available/)



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

Weak linking framework

Using optional libraries requires additional code as it makes use of [weak linking](https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPFrameworks/Concepts/WeakLinking.html)
```objc
extern int MyWeakLinkedFunction() __attribute__((weak_import));

-weak_framework <framework_name>

if (MyWeakLinkedFunction != NULL)
{
    result = MyWeakLinkedFunction();
}
```



## Check OS Support

Why do you maybe need this. 
Well if you are writing a framework or library and you started out with supporting both macOS and iOS. But while running swift DocC publisher you can try to avoid building errors for macOS target.

I encountered this problem while running https://github.com/SensehacK/swift-sense for this Swift DocC.

```swift
#if os(macOS)
func someMacOSOnlyFunction() { /* ... */ }
#endif
```

```swift
#if os(iOS)
import UIKit
public extension Image { }
#endif
```

In SwiftUI you can use this for limiting the UI as well.

```swift
NavigationLink(value: asset) {
	CustomView(asset: asset)
}
#if os(iOS)
.listRowSeparatorTint(.black)
#endif

#if os(iOS)
var drag: some Gesture {
	DragGesture()
}
#endif
```

[swift forums | if-vs-available-vs-if-available](https://forums.swift.org/t/if-vs-available-vs-if-available/40266/2)




## Check Simulator

```swift
#if targetEnvironment(simulator)
// your code
#endif
```