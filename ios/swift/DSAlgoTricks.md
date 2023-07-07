# Data Structure & Algorithm

## Intro

Sometimes I always need a refresher in how I do certain things in swift language.
And basic concepts which you always forget every now and then.
I kind of don't like leetcode centric interviews but I definitely understand its usage in backend engineering jobs or fresh junior software engineer without a computer science degree or something near Mathematical or Engineering degree.



## HashMap


```swift
func hashTable()  {
	let numbers = [1,4,5,3,3,12,3,5,3,3,6,7,1,2]
	var hashMap = [Int: Int]()
	for number in numbers {
		if (hashMap[number] != nil) {
			hashMap[number]! += 1
		} else {
			hashMap[number] = 1
		}
	}
 // hashMap
	for (keys, values) in hashMap {
		print("\(keys): \(values)")
	}
}
```

Fib 

```swift
func fibonacciSequence(n: Int) -> [Int] {
    var result: [Int] = [0,1]
    guard n > 1 else { return result }
    for _ in 0...n-2 {
        let sum = result[result.count - 2] + result.last!
        result.append(sum)
    }
    return result
}
```

## Array

```swift
for (index, value) in arrayS.enumerated() { }
for i in stride(from: 0, to: arrayValue.count, by: 1) { }
```

### 2D Array Matrix

Since you can't directly access nth or mth element in swift array. We need to first initialize the 2D array with some dummy number.

```swift
var mirrorMatrix = Array(repeating: Array(repeating: Int.max, count: input.count), count: input[0].count)
```

dynamic approach:

```swift
var matrix = [[Int]]() // creates an empty matrix
var row = [Int]() // fill this row
matrix.append(row) // add this row
```

Dynamic approach [source SO](https://stackoverflow.com/a/36655971/5177704)
## Integers

Get bit value of how many 1s are in the number in binary format
```swift
num.nonzeroBitCount
```

## Conversion

### String to Int
```swift
let myString1 = "556"
let myInt1 = Int(myString1) ?? 0
let convertedInt = try? Int(inputConcat, format: .number)
```

### String to Array
This could be necessary when you don't want to deal with string `String.Index` with accessing the nth element of String. 
The hoopla of `.index(str.startIndex, offsetBy: 3)`
Rather than dealing with these index types just convert to array. ( I know there is a conversion cost internally. )

Note: 
- Method 1: Array(String) -> This will create array of characters from string. 
- Method 2: string.split() -> This will create array of substrings from string. Easier conversion back to String after string manipulation.
```swift
// Method 1
let input: String = "Hello Kautilya!"
let strArray = Array(input)
print("Hey \(strArray[6])\(strArray[7])\(strArray[12])!")
// Hey Kay!

// Method 2
let input2: String = "Kay"
let strArray2 = input2.split(separator: "")
// ["K", "a", "y"]
```
String to characters in array [String]
```swift
var inputStrArray = stringInput.map { String($0) }
// OR you can use 
for (index, value) in stringInput.enumerated() { }
```
### Array elements to String
```swift
let array = ["1", "0", "1"] // =-> "101"
let result = array.map({$0}).joined(seperator: "")

// Method 1
let arrToCharToString = strArr.map ({ String($0) }).joined()

// Method 2
let arrToString = array.joined()

```

### Reverse a number

By utilizing multiplication and modulo operation in a while loop.
```swift
var reverseNum = 0
while(number != 0){
   reverseNum = reverseNum * 10
   reverseNum = reverseNum + number % 10
   number = number/10
}
```

Maintaining the signed integer while performing operations.
You can multiply it by `-1`

```swift
let negativeNumber = -313
var absoluteNumber = negativeNumber * -1
// OR
let positiveNumber = abs(negativeNumber)
```

Nth number elements of the array
```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
let arraySlice = names.prefix(2) // "Anna", "Alex"
let endArraySlice = names.suffix(2) // "Brian", "Jack"
names[1...3]
```

https://sarunw.com/posts/how-to-get-first-n-elements-of-swift-array/
## Sliding Window Sum


