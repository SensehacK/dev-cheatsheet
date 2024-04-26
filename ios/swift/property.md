
## Default 

```swift
let name: String = "Kautilya"
var age: Int = 28

age += 1
print("Name: " + name + " Age: " + age)
```




## Lazy Property


```swift
struct Person {
    let name: String
    let age: Int
}

struct PeopleViewModel {
    let people: [Person]
    
    lazy var oldest: Person? = {
        print("Lazy var oldest initialized")
        return people.max(by: { $0.age < $1.age })
    }()
    
    init(people: [Person]) {
        self.people = people
        print("View model initialized")
    }
}
```

[avanderlee | lazy-var-property](https://www.avanderlee.com/swift/lazy-var-property/)
