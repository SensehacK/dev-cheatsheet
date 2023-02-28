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

## Stride

```swift
for i in stride(from: 0, to: 10, by: 2) {
    print(i)
}
```

## 2D Array


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


## Reduce

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

// Note: We had to provide an optional return type of FieldFilter as we need to return nil -> which gets discarded by `CompactMap`

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

https://www.hackingwithswift.com/example-code/language/how-to-create-an-array-by-repeating-an-item

https://onmyway133.com/posts/how-to-repeat-array-of-object-in-swift/

https://qualitycoding.org/verify-arrays-approvaltests-swift/

## References

[SO](https://stackoverflow.com/questions/24781027/how-do-you-sort-an-array-of-structs-in-swift)
[Alphabetical Sort](https://stackoverflow.com/questions/46750243/sort-struct-in-alphabetical-order-swift4)