# ShortHands

It is always easier to forget which shorthands are available and sometimes you need a refresher in terms of an example with input and output.


## Map



## FlatMap


## CompactMap

Removes the nil values when working with sequence variables.




## Filter

Whatever returns a true boolean value would get filtered appropriately.
Filter works on sequence variables types like Set, Array, Dictionary.

// Even Odd example

```swift
let arr = [1, 2, 3, 4]
let evens = arr.filter { $0 % 2 == 0 }
print(evens)
```

// Struct filter
```swift
struct FieldFilter {
    let hasDynamicRecordId: Bool
    let name: String
}

let arrFields = [
    FieldFilter(hasDynamicRecordId: true, name: "Test 1"),
    FieldFilter(hasDynamicRecordId: false, name: "Test 2"),
    FieldFilter(hasDynamicRecordId: false, name: "Test 3"),
    FieldFilter(hasDynamicRecordId: true, name: "Test 4"),
    FieldFilter(hasDynamicRecordId: true, name: "Test 5"),
]

let dynamicRecordFields = arrFields.filter { $0.hasDynamicRecordId }
print(dynamicRecordFields)
```



## Note

Have added appropriate RxSwift implementations of `map, flatMap, compactMap` as well in RxSwift

## Resources

[Apple Docs](https://developer.apple.com/documentation/swift/sequence/3018365-filter)

[swiftbysundell map basics](https://www.swiftbysundell.com/basics/map-flatmap-and-compactmap/)