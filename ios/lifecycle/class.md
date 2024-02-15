# Class


## Memory Allocation


Classes (reference types) are allocated in the heap.


## Inheritance

Inheriting superclass - subclass in swift. Better explained on Apple [docs](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html)


## Multiple Inheritance

Via protocol oriented and extensions.

[Article](https://www.vadimbulavin.com/multiple-inheritance-swift/)


## Initializer Patterns


https://theswiftdev.com/swift-init-patterns/

https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/


## The self

Every instance of a type has an implicit property called `self`, which is exactly equivalent to the instance itself. You use the `self` property to refer to the current instance within its own instance methods.

https://docs.swift.org/swift-book/documentation/the-swift-programming-language/methods/#The-self-Property

## Static Final class

```swift

final class CustomClass {
	init() { }

	static func doSomethingStatic() { }

	func doNormalClassInstantiation() { }
}

let staticClass = CustomClass()
staticClass.doNormalClassInstantiation()


CustomClass.doSomethingStatic()

```

Since this static func is in `CustomClass.doSomethingStatic()` works as its own static class.

