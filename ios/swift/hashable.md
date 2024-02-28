
## Intro


## Source code

Kodeco

```swift
class Person: Equatable, Hashable {
  var name: String
  var age: Int
  init(name: String, age: Int) {
    self.name = name
    self.age = age
  }
  static func ==(lhs: Person, rhs: Person) -> Bool {
    return lhs.name == rhs.name && lhs.age == rhs.age
  }
  func hash(into hasher: inout Hasher) {
    hasher.combine(name)
    hasher.combine(age)
  }
}

let john = Person(name: "John", age: 30)
let jane = Person(name: "Jane", age: 25)

let personDict = [john: "uno", jane: "dos"]
print(personDict[jane]!) // Output: "dos"
```


## Quirks

Objective-C Interop with Swift
[NSObject subclass in Swift: hash vs hashValue, isEqual vs == ](https://stackoverflow.com/questions/33319959/nsobject-subclass-in-swift-hash-vs-hashvalue-isequal-vs)


## Resources

[Kodeco | conform-to-equatable-hashable-in-swift](https://www.kodeco.com/books/swift-cookbook/v1.0/chapters/2-conform-to-equatable-hashable-in-swift)


[Does not conform to protocol hashable](https://stackoverflow.com/questions/68893073/does-not-conform-to-protocol-hashable)
