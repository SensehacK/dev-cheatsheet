


## Intro
Initialization of any type is very important and determines how the code flow is being executed with which type of data and reference strategies.
Including the default initialization for class, structs in Swift.



## Class

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

[class](class.md)
## Struct

We don't need to specify the initializer for structs.
```swift
struct Person {
	let name: String
	let age: Int
}

let kay = Person(name: "Kautilya", age: 28)
```

[struct](struct.md)

## Static Functions
1. We can directly access the static function as if it was a class method. Like `ClassSomething.doSomething()`
2. If we want to do something in the class before initializing other stored variables / properties we can do that using a static function. Since inherently it treats itself as its own `class doSomething()`
3. Static dispatch more [performant](ios/xcode/performance#Static%20vs%20Dynamic%20dispatch) 

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




## Singleton Builder Pattern

```swift
class MySingleton {

    static let shared = MySingleton()
    
    struct Config {
        let param:String
    }
    private static var config:Config?
    
    class func setup(_ config:Config){
        MySingleton.config = config
    }
    
    private init() {
        guard let config = MySingleton.config else {
            fatalError("Error - you must call setup before accessing MySingleton.shared")
        }
        
        //Regular initialisation using config
    }
}
```

Init

```swift
MySingleton.setup(MySingleton.Config(param: "Some Param"))
```

Access Singleton

```swift
MySingleton.shared
```

[SO source](https://stackoverflow.com/questions/28429544/singleton-and-init-with-parameter)



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