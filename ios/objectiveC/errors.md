# Errors

## Property not found

Property not found on object of swift class but its internal properties aren't exposed to objective-c header / bridging interface so you need to add `@objc` property wrapper on those variables or functions to access them.

```error
error: property 'propertyName' not found on object of type 'SomeClass *'
```

```swift
public class SomeClass: NSObject {
    @objc public var propertyName: String?
    var strID: String?
}

```

##  `@objc` attribute cannot be applied

```swift
'@objc' attribute cannot be applied to this declaration
```

This error could appear when the underlying implementation is `struct` or something which is not able to be represented in Objective C bridging options.
Swift has structs but objectiveC doesn't support it directly.

A Warm Welcome to Structs and Value Types from Objc.io post
[swift-classes-vs-structs post](https://www.objc.io/issues/16-swift/swift-classes-vs-structs/)

## Support Struct in Objective C

You can wrap it as a generic value in Swift class and have the generic value as Struct

```swift
public class Box<T> {
    let unbox: T
    init(_ value: T) {
        self.unbox = value
    } }
```

[SO | how-to-pass-a-swift-struct-as-a-parameter-to-an-objective-c-method](https://stackoverflow.com/questions/28567380/how-to-pass-a-swift-struct-as-a-parameter-to-an-objective-c-method)

Things not supported by `@Objc` 

> You’ll have access to anything within a class or protocol that’s marked with the @objc attribute as long as it’s compatible with Objective-C. This excludes Swift-only features such as those listed here:
> 
> - Generics
> - Tuples
> - Enumerations defined in Swift
> - Structures defined in Swift
> - Top-level functions defined in Swift
> - Global variables defined in Swift
> - Typealiases defined in Swift
> - Swift-style variadics
> - Nested types
> - Curried functions

[SwiftObjcCocoa.pdf](https://carlosicaza.com/swiftbooks/SwiftObjcCocoa.pdf)
