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


## import swift in objective-c

Considerations - from [SO | import swift code to Objective C](https://stackoverflow.com/questions/24102104/how-can-i-import-swift-code-to-objective-c)
- If your product name contains spaces, replace them with underscores (e.g. `My Project` becomes `My_Project-Swift.h`)
- If your target is a framework, you need to import `<ProductName/ProductName-Swift.h>`
- Make sure your Swift file is a member of the target

```swift
// CFrameworkPlatform
@objc
public protocol CProtocol: AnyObject {
    func handleChange(result: String)
}
```

```objc
#import <CFrameworkPlatform/CProtocol-Swift.h>
```

Caveat if its an objectiveC inter-op from swift in a framework then it gets automatically created by xcode build process named as `customFrameworkName-Swift.h`

So you should just import it using 

```objc
#import <CFrameworkPlatform/CFrameworkPlatform-Swift.h>
```


