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

Snake case issue 

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
