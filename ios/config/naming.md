# Naming

## System namespace

Overriding the system namespace which are reserved could be avoided using backticks

```swift
public enum Bool {
	public static let `false` = "false".localized
	public static let `true` = "true".localized
}
```


## [Enum Namespacing](/ios/swift/enum#namespace)

## Avoiding name collisions

Swift LLVM gives precedence to local variables when referencing naming so that's one thing you can be cognizant about.

### Use type alias approach

TypeAlias is great way to solve full module / class namespace problem in order to make it easier for the local class / file to easily reference where the context is coming from and even is easily readable.

```swift
import customClass1
import customClass2

typealias cC1 = customClass1.doSomething
typealias cC2 = customClass2.doSomething

class DoSomething {
	func doing() {
		let cc1 = cC1()
		let cc2 = cC2()
		cc1.doSomething()
		cc2.doSomething()
	}
}
```

[usefulness-of-typealiases-in-swift](https://appventure.me/posts/2019-5-15-the-usefulness-of-typealiases-in-swift.html)

[sarunw | swift-typealias](https://sarunw.com/posts/swift-typealias/)


### Local Reference

```swift
struct CustomModule {
	var value = ""
}

struct String {
	var value = ""
}

let name1 = CustomModule()
let name2 = Swift.String()
let name3 = String()
```


### Full Module namespace

Compile error `Ambiguous use of functionName / className` eg. `doSomething()`

```swift
import customClass1
import customClass2

class DoSomething {
	func doing() {
		// Won't compile
		doSomething()
		doSomething()
		doSomethingDiff()

		// Class / Module based
		customClass1.doSomething()
		customClass2.doSomething()
		customClass2.doSomethingDiff()
	}
}
```

### Import Module namespace

Specific imports from its respective Modules. Really helpful in Framework / library driven software engineering.

```swift
import func customClass1.doSomething
import func customClass2.doSomethingDiff

class DoSomething {
	func doing() {
		doSomething()
		doSomething()
		doSomethingDiff()
	}
}
```


### Encapsulate functions in sandbox

So you can easily just move the global functions into its respective class or structs for easier namespace. If you can control the source code of the project or library you're embedding.

```swift
// CustomClass1.swift
public func doSomething() {}


// CustomClass2.swift
public func doSomething() {}

```

Encapsulate those functions in their respective classes or sandbox of your choice in order to not expose all the functions on global namespace. Which is more expensive and not recommended to pollute more options when you're designing or writing a library to be consumed.
Follows SOLID principles as well
```swift
// CustomClass1.swift
public class CustomClass1 {
	public func doSomething() {}					   
}

// CustomClass2.swift
public class CustomClass2 {
	public func doSomething() {}					   
}
```


[Ref video youtube](https://www.youtube.com/watch?v=1Ihb7OSXLeQ)



