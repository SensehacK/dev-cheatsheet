# Keychain 

## Intro

Shared Keychain to store data of the app. Specifically Username, password and UUID, access tokens.


## Guides

[Keychain](https://www.iosapptemplates.com/blog/ios-programming/keychain-swift-ios)

Good library 
[KeychainSwift](https://github.com/evgenyneu/keychain-swift)

Better documentation with this library.
[github | KeychainAccess](https://github.com/kishikawakatsumi/KeychainAccess)

## Why

You can use Keychain to keep persistence over app installs / uninstalls in order to uniquely identify whether the app was ever used by the end user. Given that they don't reset their device which clears out the keychain entry. Could be a stop gap to implement trial check being used previously by that end user.

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



## Unique tracking 

[apple dev | post | DTS](https://developer.apple.com/forums/thread/98398?answerId=761461022#761461022)
Copied from this link ^ 

In that case the trick is to entangle your credential with a value that’s deleted when the app is deleted. I mentioned that in the [post I referenced above](https://developer.apple.com/forums/thread/36442?answerId=281900022#281900022) but let’s explore a concrete example:

Let’s say the user’s password is `opendoor`, or 6F70656E646F6F72 as UTF-8 encoded bytes. Generate a random sequence of bytes of the same length, like 1B6067C70711D099 and store that in a file in your app’s container. Now XOR the password with the random bytes and store that in the keychain. There are now four interesting cases:

- In the normal case, when you go to read the password, read the value from the keychain and the random bytes from the file, XOR them, and you have the original password.
    
- If the user deletes your app, the file is removed and the item in the keychain becomes useless.
    
- If the user deletes your app and re-installs it, the keychain item will be there but the file won’t be. In that case the password is lost.
    
- It’s also possible that the user might have managed to migrate your app such that the file is present but the keychain item isn’t. In the case the password is lost as well.

## References

[dev apple | keychain_services](https://developer.apple.com/documentation/security/keychain_services)


[apple dev forums | eskimo | post basics of SecItem | Keychain API](https://developer.apple.com/forums/thread/724023)

[SO | diff between userdefaults and keychain](https://stackoverflow.com/questions/12090136/difference-between-keychain-and-nsuserdefault)
