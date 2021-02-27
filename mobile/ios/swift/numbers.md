# Numbers


## Int


## Decimal


## Parsing

Error: Initializer 'init(_:)' requires that 'Decimal' conform to 'BinaryInteger'
```swift
var integer = 0
let temp = Decimal(value) * (pow(10, digits.count-index-1))
print(type(of: temp)) // prints ** NSDecimal **

integer += Int(truncating: temp as NSNumber)

```
[SO](https://stackoverflow.com/questions/61090503/initializer-init-requires-that-decimal-conform-to-binaryinteger)


// Converting NSDecimal to Int

```swift
let size = Decimal(2)
let test = pow(size, 2) - 1
let result = NSDecimalNumber(decimal: test)
print(Int(result)) // testing the cast to Int
```

[SO](https://stackoverflow.com/questions/39731265/swift-3-decimal-to-int)