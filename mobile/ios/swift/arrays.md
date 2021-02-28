# Arrays


## Init


## 2D Array

[HWS](https://www.hackingwithswift.com/example-code/arrays/how-do-you-create-multi-dimensional-arrays)

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

## References

[SO](https://stackoverflow.com/questions/24781027/how-do-you-sort-an-array-of-structs-in-swift)