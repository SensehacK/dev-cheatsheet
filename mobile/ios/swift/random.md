# Random

## Generate Random numbers


```swift 
let randomInt = Int.random(in: 1..<5)
let randomFloat = Float.random(in: 1..<10)
let randomDouble = Double.random(in: 1...100)
let randomCGFloat = CGFloat.random(in: 1...1000)
let randomBool = Bool.random()
```


## Shuffle array


```swift

let numbers = [1, 2, 3]
let shuffledNumbers = (numbers as NSArray).shuffled() as! [Int]

```


## Random element in array

```swift

var albums = ["Slim Shady LP", "GKMC", "2014 Forest Hills Drive"]


if let random = albums.randomElement() {
    print("The random album is \(random).")
}

```

## UUID

Random UUID

```swift

UUID().uuidString
// Example Output:
// 25A4DA38-743C-46D0-9B71-1699556C975E

```



## Enum Random

Random Enum

One implementation to get a random enum requires the enum to conform to the CaseIterable protocol. In this example, the enum Assignment is defined to conform to CaseIterable:

```swift
enum Assignment: CaseIterable {
    case coding
    case debugging
    case ui
    case testing
    case documentation
    case refactoring
}

```

Another option is to extend an enum to conform to CaseIterable. The CaseIterable protocol has no required methods so only the extension statement is required:

```
extension Assignment: CaseIterable {}
Assignment.allCases.randomElement()
// Example Output: .testing
```
Enums that conforms to CaseIterable gain an allCases property containing a list of all the available enum cases. To get a random enum, call randomElement() on allCases:


[Hacking With Swift](https://www.hackingwithswift.com/articles/102/how-to-generate-random-numbers-in-swift)

[Advance Swift](https://www.advancedswift.com/swift-random-numbers/)


Note: I believe most of the things here are copied & I didn't create this file documentation examples. I'm still keeping this in case I need offline access and fast search in iA Writer.