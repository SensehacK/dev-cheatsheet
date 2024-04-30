# Codable

## Tool

Quickly type JSON structs for Swift or any other languages. Network Models

https://app.quicktype.io/

## UserDefaults

Codable Property Wrapper
On iOS 12 and prior, primitive types (Int, Double, Bool, etc), while Codable
as a property of a Codable type, cannot itself be JSON encodable. Trying encoding/decoding with these types on iOS 12 earlier platforms will throw an error.
To remedy this behavior we wrap the Codable value in a simple Codable struct.

User Defaults example usage

```swift
@propertyWrapper
public struct UserDefaultsBacked<Value: Codable> {
private let key: String
private let defaultValue: Value
private let domain: UserDefaults
public var wrappedValue: Value { }

public init(key: String, defaultValue: Value, domain: UserDefaults = .standard) {
	self.key = key
	self.defaultValue = defaultValue
	self.domain = domain
}
```

```swift
struct Wrapper<Value>: Codable where Value: Codable {
	let value: Value
}

// Wrapped value
// GET
do {
	let wrappedValue = try JSONDecoder().decode(Wrapper<Value>.self, from: data)
	return wrappedValue.value
}

// SET
set {
	do {
		let data = try JSONEncoder().encode(Wrapper(value: newValue))
		domain.setValue(data, forKey: key)
	} catch {}
}
```


## Decoder

### Snake case issue 

```sh
ERROR: keyNotFound(CodingKeys(stringValue: "iso_3166_1", intValue: nil)
```
Just use 
`.convertFromSnakeCase` for decoder strategy

```swift
let decoder = JSONDecoder()
decoder.keyDecodingStrategy = .convertFromSnakeCase
```

[SO | swiftui-get-error-when-decoding-json-data-which-includes-key-name-as-iso](https://stackoverflow.com/questions/61378814/swiftui-get-error-when-decoding-json-data-which-includes-key-name-as-iso-3166)


### The data couldn’t be read because it isn’t in the correct format.


```log
dataCorrupted(Swift.DecodingError.Context(codingPath: [_JSONKey(stringValue: "", intValue: 0), CodingKeys(stringValue: "TestKey", intValue: nil)], debugDescription: "Cannot initialize  TestKey from invalid String value TestValue", underlyingError: nil))
```

This probably happen because the API changed few things on their backend and you should have had optional initializers rather than concrete tie-ins. this resulted in full failure from the client consumer side of things and it led to your app / software in broken state. Very bad design but I was working around a POC and I just wanted to build something quickly.



## Troubleshooting coding / decoding errors


When using `JSONDecoder` or `.decode()` functions, make sure you have do try catch added explicitly so that it doesn't fail silently with those JSON coding / decoding views.

Make sure to use `String(describing:)` as well instead of `.localizedDescriptions`

[SO snippet](https://stackoverflow.com/a/68044439/5177704)
```swift
do {
    let decoded = try JSONDecoder().decode([Struct].self, from: data!)
} catch {
    // print(error.localizedDescription) // <- ⚠️ Don't use this!
    print(String(describing: error)) // <- ✅ Use this for debuging!
}
```