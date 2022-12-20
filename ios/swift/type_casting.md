# Type Casting

Forced type casting (as!)

Conditional type casting (as?)

[Type Casting](https://learnappmaking.com/type-casting-swift-how-to/)

https://medium.com/swlh/type-casting-in-swift-bd99a68d0845


https://thisdevbrain.com/how-to-convert-a-string-to-a-custom-type-in-swift/


## Dictionary Types Casting

Converting from [String: Any] => [String: String]
Using **LosslessStringConvertible** in
-   Bool
-   Double
-   Float
-   Float80
-   Path
-   Substring
-   Unicode.Scalar

`String(describing: CustomStringConvertible)`

```swift
let people: [String: Any] = ["Taylor": 178.0, "Justin": 175, "Ed": 173.23, "Nick": true, "Lexton": "Son"]
let peopleValue = people.mapValues { String(describing: $0) }

// ["Nick": "true", "Taylor": "178.0", "Justin": "175", "Ed": "173.23", "Lexton": "Son"]
```

https://daddycoding.com/2020/02/17/converting-string-any-to-string-string/