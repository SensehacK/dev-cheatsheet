
## Intro
Needed for comparing objects with internal custom properties at developer's business logic expense.


## Code 
```swift
class Person {
  var name: String
  var age: Int
  init(name: String, age: Int) {
    self.name = name
    self.age = age
  }
}

extension Person: Equatable {
  static func ==(lhs: Person, rhs: Person) -> Bool {
    return lhs.name == rhs.name && lhs.age == rhs.age
  }
}

let person1 = Person(name: "John", age: 30)
let person2 = Person(name: "John", age: 30)
let person3 = Person(name: "Jane", age: 25)
print(person1 == person2) // true
print(person1 == person3) // false
```


## Objective C | NSObject | isEqual | ==

Because your class inherits from `NSObject` you do not need to use the swift protocol `Equatable` instead you must override the `NSObject` method `isEquals`:


Code Snippet
```swift
class Person: NSObject, NSCoding {
	var name: String
	var age: String
	init(name: String, age: Int) {
	    self.name = name
	    self.age = age
	}
	
	override func isEqual(_ object: Any?) -> Bool {
	    return name == (object as? Person)?.name
	}
}
```
[SO post link](https://stackoverflow.com/questions/37085839/overridden-function-for-equatable-type-not-called-for-custom-class-that-subcl)

https://stackoverflow.com/questions/37390172/redundant-conformance-of-generic-to-protocol-equatable-in-swift-2-2
## Resources

https://www.avanderlee.com/swift/equatable-comparible-conformance/