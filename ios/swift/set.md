# Set

Unique elements internally. Unordered by definition because it internally does hashing to uniquely reference its elements. So it has O(n) time complexity for reading a value or referencing a value.

## Init

Create a set 

```swift
let customSet:Set<Int> = Set<Int>(1,3,5,8,4)
```

## Venn Diagrams

You can utilize different functions around Sets with in relation to venn diagrams


## Convert Array to Set

Code snippet 
```swift
let numbers = [30, 50, 20, 80, 50, 90, 40, 30]
print("Array: ", numbers)

// Converting
let rSet = Set(numbers)
print("Set:", rSet)
```