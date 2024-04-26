# Arrays


## Init



## Join

```swift
let strArray = ["My", "Name", "is", "Kautilya", "Save"]
let combinedString = strArray.joined(separator: ", ")
print("Combined String", +combinedString)
```


## Sort

Full declaration
```swift
myArr.sort { (lhs: EntryStruct, rhs: EntryStruct) -> Bool in
    // you can have additional code here
    return lhs.deadline < rhs.deadline
}

// OR

let newArr = myArr.sorted { (lhs: EntryStruct, rhs: EntryStruct) -> Bool in
    // you can have additional code here
    return lhs.deadline < rhs.deadline
}
```

Compact declaration

```swift
myArr.sort { $0.deadline < $1.deadline }

//OR

let newArr = myArr.sorted { $0.deadline < $1.deadline }
```


## Multiple Sort

Sorting arrays via multiple checks.

Code snippet from [sarunw | sort multiple properties swift](https://sarunw.com/posts/how-to-sort-by-multiple-properties-in-swift/)

```swift
extension BlogPost {    
	static var examples2: [BlogPost] = [
	BlogPost(title: "Zoo", pageView: 5, sessionDuration: 2),
	BlogPost(title: "Alice", pageView: 1, sessionDuration: 3),
	BlogPost(title: "Peter", pageView: 1, sessionDuration: 2),  
	BlogPost(title: "Kofi", pageView: 1, sessionDuration: 1),   
	BlogPost(title: "Akosua", pageView: 5, sessionDuration: 2), 
	BlogPost(title: "Abena", pageView: 4, sessionDuration: 10),  
	BlogPost(title: "Angero", pageView: 1, sessionDuration: 2)    ]
}

typealias AreInIncreasingOrder = (BlogPost, BlogPost) -> Bool // <1>    

let popularPosts = BlogPost.examples2.sorted { (lhs, rhs) in  let predicates: [AreInIncreasingOrder] = [
	{ $0.pageView > $1.pageView }, 
	{ $0.sessionDuration > $1.sessionDuration},
	{ $0.title < $1.title }
 ]      
 for predicate in predicates { 
	if !predicate(lhs, rhs) && !predicate(rhs, lhs) { 
		continue  
	}                
	return predicate(lhs, rhs)
 }        
  return false
}
```


## Stride

```swift
for i in stride(from: 0, to: 10, by: 2) {
    print(i)
}
```

## Continue || Break

Print odd numbers only and skip even numbers. We can ofcourse flip the condition with just 1 if condition for print(i) but my example wanted to include something for `continue` and `break`
```swift
for i in stride(from: 0, to: 15, by: 1) {
	if i % 2 == 0 {
		continue
	} else {
		print(i)
	}

	if i == 7 {
		print("Found the lucky number!")
		break
	}
}
```

## 2D Array

Creating 2D matrix array in Swift.

```swift
// Create a constant, jagged array.
let units: [[Int]] = [
[100, 200, 300],
[400, 500], [600],
[700, 800], [900]
]

// Loop over array and all nested arrays.
for var x in 0..<units.count {
    var line = ""
    for var y in 0..<units[x].count {
        line += String(units[x][y])
        line += " "
    }
    print(line)
}
```

[HWS](https://www.hackingwithswift.com/example-code/arrays/how-do-you-create-multi-dimensional-arrays)
[2D Array](https://www.dotnetperls.com/2d-swift)

## Array to Number

```swift
func plusOne(_ digits: [Int]) -> [Int] {
    var arrayD:[Int] = []   
    var integer = 0
    for (index,value) in digits.enumerated() {
		let multiplier = pow(10, digits.count-index-1)
        let temp = Decimal(value) * (pow(10, digits.count-index-1))
        print(temp)
        print(type(of: temp))
        integer += Int(truncating: temp as NSNumber)
    }
    print(integer)
    return arrayD
    }
}
```

## Data

```swift
let arrFields = [
    FieldFilter(hasDynamicRecordId: true, name: "Test 1"),
    FieldFilter(hasDynamicRecordId: false, name: "Test 2"),
    FieldFilter(hasDynamicRecordId: false, name: "Test 3"),
    FieldFilter(hasDynamicRecordId: true, name: "Test 4"),
    FieldFilter(hasDynamicRecordId: true, name: "Test 5"),
]
```

## Map

Makes mapping every element easier on the contiguous data structure.

```swift
let cast = ["Viv", "Darlon", "Fim", "Carl"]
let lowercaseNames = cast.map { $0.lowercased() }
let letterCounts = cast.map { $0.count }
```

[Apple Dev | map](<https://developer.apple.com/documentation/swift/array/map(_:)-87c4d>)

## Reduce


```swift
let booleans = [true, true, false, true, false]
let result = booleans.reduce(true, { $0 && $1 })
print(result) // false

// Another variant 
let numbers = [1, 34, 35, 64, 2]
let result = numbers.reduce(into: 0) { $0 += $1 }
let result2 = numbers.reduce(0, +)
```

### `reduce(into:_:_)` vs `reduce(:_:_)`

```swift
let result = numbers.reduce(into: 0) { $0 += $1 }
// VS
let result4 = numbers.reduce(0) { $0 + $1 }
```
`reduce(into:_:_)`
One works with `+=` because those are `&inOut` variables which lets us have mutable state for avoiding Copy On Write (CoW) from Swift.

`reduce(:_:_)`
With normal `reduce(:_:_)` it creates a immutable variables to store the new result every time the loop increments.

[Apple dev | reduce](<https://developer.apple.com/documentation/swift/array/reduce(into:_:)>)

[Reduce function](https://medium.com/@lucianoalmeida1/a-little-bit-about-the-cool-reduce-in-swift-306edd9ceb57)


## Filter

```swift
// Even Odd example
let arr = [1, 2, 3, 4]
let evens = arr.filter { $0 % 2 == 0 }
print(evens)
```


```swift
print("\n Using Filter")
let filterDynamicRecordFields = arrFields.filter { $0.hasDynamicRecordId }
print(filterDynamicRecordFields)

```


## Compact Map

Note: We had to provide an optional return type of FieldFilter as we need to return nil -> which gets discarded by `CompactMap`

```swift
print("\n Using Compact Map")
let compactMapDynamicRecordFields = arrFields.compactMap { fieldFilter -> FieldFilter? in
    guard fieldFilter.hasDynamicRecordId else { return nil }
    return fieldFilter
}
print(compactMapDynamicRecordFields)
```

## Repeated Elements

We could need dummy data to be able to compared against the output. We can quickly do an array of repeating values over `n` times. 

Rather than going through the classic logic of making a `for loop` with `i = starting index` till `n = ending index` and incrementing the `i+1 = starting index with certain values` we can directly utilize `stride` or convenience initializer for every primitive Array types
`[Type](repeating: Type.Value, count: N-times)` 

```swift
let expectedResult = [Bool](repeating: true, count: 3)\

print(expectedResult) // [true, true, true]
```
[HwS | how-to-create-an-array-by-repeating-an-item](https://www.hackingwithswift.com/example-code/language/how-to-create-an-array-by-repeating-an-item)

[how-to-repeat-array-of-object-in-swift](https://onmyway133.com/posts/how-to-repeat-array-of-object-in-swift/)

[verify-arrays-approvaltests-swift](https://qualitycoding.org/verify-arrays-approvaltests-swift/)

[13-useful-array-methods-in-swift](https://betterprogramming.pub/13-useful-array-methods-in-swift-e169a78cba8d)

## Extensions

### Does Not Contains
Opposite of `contains` check and could be properly named as `excludes` == !contains()
```swift
extension Sequence where Element: Equatable {
    
    func doesNotContains(_ element: Element) -> Bool {
        return !self.contains(element)
    }
}
```


## References

[SO | Sort array](https://stackoverflow.com/questions/24781027/how-do-you-sort-an-array-of-structs-in-swift)

[SO | Alphabetical Sort](https://stackoverflow.com/questions/46750243/sort-struct-in-alphabetical-order-swift4)