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


### Keys

Good way to define keys in order to access them whenever needed.

```swift
enum Keys {
	static let isLoggedIn = "AppName.State.isLoggedIn"
	static let colorScheme = "AppName.Pref.colorScheme"
}
```


## Manager


```swift
class UserDefaultsManager {
	private let defaults = UserDefaults.standard
    
    // Singleton
    static var shared: UserDefaultsManager = UserDefaultsManager()
    private init() { }
    
    // MARK: - Public methods
    func get(key: UserDefaultsKey) -> String? {
        guard let returnedValue = defaults.object(forKey: key.rawValue) as? String else { return nil }
        return returnedValue
    }

    func set(key: UserDefaultsKey, value: String) {
        defaults.set(value, forKey: key.rawValue)
    }
```

## Limitations

> First and foremost, encryption - UserDefaults does not use encryption out of the box.
   
> Second, on any device a user can access the files system and specifically your app container and hence the UserDefaults using iExplorer app for example and access the whole plist that represents the user defaults - change it and extract information - not protected against malicious users.

> Third, third party libraries you are using in your app are able to access your ‘standard’ user defaults or guess some container name you are using to extract/ override the information.

[SO | link](https://stackoverflow.com/a/68022332/5177704)