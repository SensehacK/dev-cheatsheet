# User Defaults


To print the path where the plist file is stored in the iOS simulator.

```swift
let library_path = NSSearchPathForDirectoriesInDomains(.libraryDirectory, .userDomainMask, true)[0]

print("library path is \(library_path)")

```

[Persisting data](https://fluffy.es/persist-data/)

[SO](https://stackoverflow.com/questions/12525474/nsuserdefaults-or-keychain-is-better-to-save-username-and-password-in-iphone-app#12525551)

[Swift guide](https://www.simpleswiftguide.com/how-to-use-userdefaults-in-swift/)

## Custom dictionary

Specify which part of data would be under a certain class name / struct. 


`NSHomeDirectory()`

https://crystalminds.medium.com/where-are-the-standard-userdefaults-stored-d02bf74854ff

Note about User Defaults drawbacks.
https://www.hackingwithswift.com/guide/ios-swiftui/4/2/key-points
