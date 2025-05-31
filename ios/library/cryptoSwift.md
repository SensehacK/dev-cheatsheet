# Crypto Swift

Utilizing Crypto Swift library to store our encryption data values in keychain for basic cryptography for the app.
Advanced Encryption Standard (AES)

## Protocols 

```swift
protocol Encryptable { 
	func encrypt(value: String?) -> String?
	func decrypt(encryptedValue: String?) -> String?
	func clear()
}
```

## Enum

```swift
enum Keys {
	static let AESIV = "AESEncrypt.Keys.Iv"
	static let AESKey = "AESEncrypt.Keys.cipher"
}
```

## Manager

```swift
final class AESCrypto: Encryptable {
	// Define some Keychain Keys

	// Singleton
	public static let shared = AESCrypto()
	private init() {}

	// Private Properties
	private var _aesVector: String?
	private var _aesKey: String?
	private var _cipher: AES?
}
```

## Generate a Vector

```swift
let vector = AES.randomIV(AES.blockSize).toBase64()
```

Good way to store the AES random vector is in Keychain.

## Generate a Key

```swift
func generateKey() -> String? {
	let aesData = Data(count: AESEncryptionByteLength.aes256.rawValue)
	var modifiedData = aesData
	let _ = modifiedData.withUnsafeMutableBytes { mutableBytes in
		SecRandomCopyBytes(kSecRandomDefault, aesData.count, mutableBytes)
	}
	return modifiedData.bytes.toBase64()						   
}
```

Good way to store the AES random vector is in Keychain.


## Retrieving Initial Key
Randomly generate initialization vector for encryption, decryption. Store this is Keychain.

```swift
var aesKey: String? {
	// Return if device is unlocked.
	guard KeychainManager.shared.checkAccessible(key: Keys.AESKey) else { return nil }

	// check whether it is stored in Keychain & if not nil returned
	guard let aesKey = _aesKey ?? KeychainManager.shared.get(key: Keys.AESKey) else {
		// Generate a new one ^ Refer one above & store in Keychain
		if let newAESKey = generateKey() {
			KeychainManager.shared.set(key: Keys.AESKey, values: newAESKey)
			_aesKey = newAESKey
		}
		return _aesKey
	}
	_aesKey = aesKey
	return _aesKey
}
```
## Retrieving Initial Vector
Randomly generate initialization vector for encryption, decryption. Store this is Keychain.

```swift
var aesVector: String! {
	// Return if it already exists
	if _aesVector { _aesVector }

	// check whether it is stored in Keychain & if not nil returned
	if _aesVector = KeychainManager.shared.get(key: Keys.AESIV) {
		return _aesVector
	}

	// Generate a new one ^ Refer one above.
	KeychainManager.shared.set(key: Keys.AESIV, values: vector)
	_aesVector = vector
	return _aesVector
}
```

## Generate Cipher Instance

```swift
var aesCipher: AES? {
	// Return if it already exists
	if _cipher { _cipher }

	// Generate a new one 
	guard 
	let key =  aesKey, 
	let vector = aesVector, 
	let keyData = Data(base64Encoded: key)?.bytes,
	let vectorData = Data(base64Encoded: vector)?.bytes else { return nil }

	_cipher = try? AES(key: keyData, blockMode: CBC(iv: vectorData), padding: .pkcs5)
	return _cipher
}
```


## Protocol Methods

Conformance of protocol with the class
```swift
final class AESCrypto: Encryptable { }
```

### Encrypt 

```swift
public func encrypt(value: String?) -> String? {
	guard
		let value = value,
		let aesCipher = aesCipher,
		let data = value.data(using: .utf8),
		let result = try? data.encrypt(cipher: aesCipher) else {
		return nil
	}
	// Return the encrypted value
	return result.base64EncodedString()
}
```

### Decrypt

```swift
public func decrypt(encryptedValue: String?) -> String? {
	guard
		let eValue = encryptedValue,
		let aesCipher = aesCipher,
		let data = Data(base64Encoded: eValue),
		let result = try? data.decrypt(cipher: aesCipher) else {
		return nil
	}
	// Return the decrypted value
	return String(bytes: result, encoding: .utf8)
}
```

### Clear

```swift
func clear() {
	KeychainManager.shared.delete(key: Keys.AESKey)
	KeychainManager.shared.delete(key: Keys.AESIV)
	_aesVector = nil
	_aesKey = nil
	_cipher = nil		  
}
```


## References

[cryptoswift.io](https://cryptoswift.io/)
