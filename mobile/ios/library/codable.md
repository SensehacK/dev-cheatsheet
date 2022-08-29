

## UserDefaults Codable Wrapper

On iOS 12 and prior, primitive types (Int, Double, Bool, etc), while Codable
as a property of a Codable type, cannot itself be JSON encodable. Trying encoding/decoding with these types on iOS 12 earlier platforms will throw an error.
To remedy this behavior we wrap the Codable value in a simple Codable struct.


User Defaults example
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




```swift
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
