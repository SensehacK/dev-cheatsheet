# Dictionary


## Init

Different types to initialize
```swift
let dict = [String: Int]()

let dict2: [String: Int] = [
		"Kautilya": 0,
		"Zeus": 1,
		"Sensehack": 2,
]

let dict3: [String: Int]?

var initProtocol = [String : Int]()
someProtocol["one"] = 1
someProtocol["two"] = 2

let someProtocol = [
    "one" : 1,
    "two" : 2
]
```


## Access

Traversing
```swift
for (key, value) in dictionaryName {
		// Depending on types you would parse or type cast these data types while printing or utilizing.
    print("Key: \(key) & value: \(value)")
}
```

## Complexity

Search: 
Searching time is always constant in Dictionary as they are hashed internally, so the key is accepted in any common hashable data type and Swift compiler internally generates a Hash value for it. So it’s easy to get those details. 

Quirks: 
Thats the reason that Dictionary aren’t organized in a sorted manner.

Update: It’s also in constant Big O(1) time.


## Applications

- Great for generating a hash map or keeping track of things in computer science.
- Different data types can be utilized. 
- Great for real life enterprise scenarios where restful APIs returns a mix of primitive types in JSON data format.

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
        
//        hashMap
        
        
        for (keys, values) in hashMap {
            print("\(keys): \(values)")
        }
    }


```
## References

[SO](https://stackoverflow.com/questions/44637836/what-is-the-equivalent-of-a-java-hashmapstring-integer-in-swift)

[Tutorials Point](https://www.tutorialspoint.com/swift/swift_dictionaries.htm)