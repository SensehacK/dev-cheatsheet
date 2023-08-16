
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

