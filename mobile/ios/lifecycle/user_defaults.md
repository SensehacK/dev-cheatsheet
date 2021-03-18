# User Defaults


To print the path where the plist file is stored in the iOS simulator.

```swift
let library_path = NSSearchPathForDirectoriesInDomains(.libraryDirectory, .userDomainMask, true)[0]

print("library path is \(library_path)")

```

[Persisting data](https://fluffy.es/persist-data/)

[SO](https://stackoverflow.com/questions/12525474/nsuserdefaults-or-keychain-is-better-to-save-username-and-password-in-iphone-app#12525551)