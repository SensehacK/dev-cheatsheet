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

### Search
Searching time is always constant in Dictionary as they are hashed internally, so the key is accepted in any common hashable data type and Swift compiler internally generates a Hash value for it. So it’s easy to get those details. 

### Quirks
Thats the reason that Dictionary aren’t organized in a sorted manner.

### Update
It’s also in constant Big O(1) time.


## Applications

- Great for generating a hash map or keeping track of things in computer science.
- Different data types can be utilized. 
- Great for real life enterprise scenarios where restful APIs returns a mix of primitive types in JSON data format.



## convert Dictionary Values to Array

Could be replaced with compactMap { $0 } as well
```swift
let colors = colorsForColorScheme.values.flatMap { $0 }
```
Or 
```swift
let colors = Array(dict.values)
```
Or 
```swift
let colors = colorsForColorScheme.map { $0.1 }
```


## Flat Map

[SO | Post](https://stackoverflow.com/questions/35597850/swift-flatten-an-array-of-dictionaries-to-one-dictionary)

## Bool check func

```swift
var disablePlaybackEndEvent =  [
        AssetClass.livod: true,
        AssetClass.vod: true,
]
var currentAssetClass = AssetClass.ivod
func shouldDeferEvent() -> Bool {
	guard let emitResult = disablePlaybackEndEvent[currentAssetClass] else { return false }
	return emitResult
}
```
## References

[SO](https://stackoverflow.com/questions/44637836/what-is-the-equivalent-of-a-java-hashmapstring-integer-in-swift)

[Tutorials Point](https://www.tutorialspoint.com/swift/swift_dictionaries.htm)

[SO | swift-dictionary-get-values-as-array](https://stackoverflow.com/questions/26988167/swift-dictionary-get-values-as-array)

