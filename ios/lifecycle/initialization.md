


## Intro
Initialization of any type is very important and determines how the code flow is being executed with which type of data and reference strategies.
Including the default initialization for class, structs in Swift.



## [Class](/ios/lifecycle/class.md)

We need to specify the initializer for class.
```swift
class Person {
	let name: String
	let age: Int

	init(name: String, age: Int) {
		self.name = name
		self.age = age
	}

}

let kay = Person(name: "Kautilya", age: 28)
```


## [Struct](struct.md)

We don't need to specify the initializer for structs.
```swift
struct Person {
	let name: String
	let age: Int
}

let kay = Person(name: "Kautilya", age: 28)
```



## Static Functions
1. We can directly access the static function as if it was a class method. Like `ClassSomething.doSomething()`
2. If we want to do something in the class before initializing other stored variables / properties we can do that using a static function. Since inherently it treats itself as its own `class doSomething()`
3. Static dispatch more [performant](/ios/xcode/performance#Static%20vs%20Dynamic%20dispatch) 

```swift
class ClassSomething {
	let desc: String

	init() {
		let storedValue = Self.doSomething()
		desc = storedValue ? "We Got Some" : "None"
	}
	
	static func doSomething() -> Bool {
		return true
	}
}
```

## [Singleton Pattern](/ios/lifecycle/singleton_pattern.md)



## Property Getter and Setters 


```swift
class Temperature {
    var celsius: Float = 0.0
    var fahrenheit: Float {
        get {
            ((celsius * 1.8) + 32.0)
        }
        set(temp) {
            celsius = (temp - 32)/1.8
        }
    }
}

let temp = Temperature()
temp.fahrenheit = 99
print (temp.celsius)
```


## Reflection

Objective C chops

```swift
var className = "YourAppName.TestViewController"
let aClass = NSClassFromString(className) as! UIViewController.Type
let viewController = aClass()
```

Check if the class is present or instantiated in Runtime

```swift
@objc enum SDK: Int {
	case Custom1 = 0
	case Custom2

	var isInstantiated: Bool {
		switch self {
		case SDK.Custom1:
		return NSClassFromString("Custom1_Lib_Name") != nil
		case SDK.Custom2:
		return NSClassFromString("Custom2_Lib_Name") != nil
		}
	}
}
```

[apple doc | NSClassFromString](https://developer.apple.com/documentation/foundation/1395135-nsclassfromstring?language=objc)


