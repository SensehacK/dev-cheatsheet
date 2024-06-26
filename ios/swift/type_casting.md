# Type Casting

Forced type casting (as!)

Conditional type casting (as?)

[Type Casting](https://learnappmaking.com/type-casting-swift-how-to/)

[medium | type-casting-in-swift](https://medium.com/swlh/type-casting-in-swift-bd99a68d0845)

[how-to-convert-a-string-to-a-custom-type-in-swift](https://thisdevbrain.com/how-to-convert-a-string-to-a-custom-type-in-swift/)


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
[converting-string-any-to-string-string](https://daddycoding.com/2020/02/17/converting-string-any-to-string-string/)



 [Existential any](any.md)

##  Converting to Data


```swift
let cafe: Data? = "Café".data(using: .utf8) // non-nil
```
[string-to-data-and-back](https://www.objc.io/blog/2018/02/13/string-to-data-and-back/)


[medium | JSON data Dictionary parsing](https://medium.com/@lukesimoncurtis/parsing-json-to-dictionary-in-swift-4-from-an-api-3589df6aa5cf)
