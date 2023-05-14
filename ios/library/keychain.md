# Keychain 

Shared Keychain to store data of the app. Specifically Username, password and UUID, access tokens.

[Keychain](https://www.iosapptemplates.com/blog/ios-programming/keychain-swift-ios)

Good library 
[KeychainSwift](https://github.com/evgenyneu/keychain-swift)

Better documentation with this library.
https://github.com/kishikawakatsumi/KeychainAccess



### Keys

Good way to define keys in order to access them whenever needed.

```swift
enum Keys {
	static let accessToken = "AppName.Token.access"
	static let refreshToken = "AppName.Token.refresh"
}
```



## Keychain is accessible

```swift
/// Check `OSStatus` is not equal to some error
func checkAccessible(key: String) -> Bool {
	_ = KeychainManager.get(key)
	return keychainManager.result != errSecInteractionNotAllowed
}
```