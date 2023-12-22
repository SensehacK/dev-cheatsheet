# Optionals

## Declaration

```swift
var gender: String?

struct Person {
	let name: String
	var age: Int?
	var gender: String?
}
```

Accessing optionals

```swift
print(gender)

let p1 = Person(name: "Kay", age: nil, gender: nil)
print(p1.age) // prints `nil`
```

Defining the Person property optional and now we have to always resort to using `?` to access its parameters. I believe it is called `optional chaining` I'm not sure.

```swift
let p2: Person?

p2 = Person(name: "Bay", age: 24, gender: nil)
print(p2?.name) // Optional ("Bay")
print(p2?.age) // Optional (24)
```

## If Let 

```swift
if let p2 {
	print(p2.name)
	print(p2.age)
}
```

## Guard optionals

```swift
guard let p2 else { return }
print(p2.name)
print(p2.age)

```

## Code Example

```swift
struct VSS: Equatable {
    var contentID: String?
    var streamID: String?
    var streamSignal: String?
}

class Trial {
    private var previousVSS: VSS? = nil
    
    init() { testSomething() }
    
    
    func testSomething() {
        if previousVSS == nil {
            previousVSS = VSS(contentID: "asga2", streamID: nil, streamSignal: nil)
            previousVSS = VSS(contentID: previousVSS?.contentID, streamID: "@31r", streamSignal: "312r3d")
        }
        
        print(previousVSS?.contentID)
        print(previousVSS)
    }
}

let _ = Trial()
```

## References

[extending-optionals-in-swift](https://www.swiftbysundell.com/articles/extending-optionals-in-swift/)
