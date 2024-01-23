# Interoperability with Swift


## Intro

Swift keywords for inter-op with Objective-C
[dynamic_runtime](dynamic_runtime.md)

[swift-objective-c-interoperability-and-best-practices](https://infinum.com/handbook/ios/miscellaneous/swift-objective-c-interoperability-and-best-practices)



## Bridge header

Creating a bridge header for connecting both swift & objective c environment which could be auto prompted by Xcode.

Also swift won’t have to import in independent files with .swift file extension. It gets auto imported from bridge header file.
[SO](https://stackoverflow.com/questions/24002369/how-do-i-call-objective-c-code-from-swift?)

## Swift to Objc Bridge

Class

```swift
class SomeClass { }
// bridge to Obj-C
class SomeClass: NSObject { }
```

Methods & Variables

```swift
func someMethod { }
// bridge to Obj-C
@objc 
func someMethod{ }


var contentID: String?
// bridge to Obj-C
@objc 
var contentID: String?
```

Protocol Interface

```swift
public protocol CSSDelegate: AnyObject {
    func handleChange(result: SomeClass)
}
// bridge to Obj-C
@objc
public protocol CSSDelegate: AnyObject {
    func handleChange(result: SomeClass)
}
```






## Adding Objective-C to Swift codebase

[SO | how-do-i-call-objective-c-code-from-swift](https://stackoverflow.com/questions/24002369/how-do-i-call-objective-c-code-from-swift)

