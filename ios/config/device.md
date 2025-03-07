
## Code

```swift
UIDevice.current.userInterfaceIdiom == .pad
UIDevice.current.userInterfaceIdiom == .phone
UIDevice.current.userInterfaceIdiom == .unspecified
```

## Model

```swift
public extension UIDevice {
    static let modelName: String = {
        var systemInfo = utsname()
        uname(&systemInfo)
        let machineMirror = Mirror(reflecting: systemInfo.machine)
        let identifier = machineMirror.children.reduce("") { identifier, element in
            guard let value = element.value as? Int8, value != 0 else { return identifier }
            return identifier + String(UnicodeScalar(UInt8(value)))
    }
}
```

1. POSIX defines [`struct utsname`](http://pubs.opengroup.org/onlinepubs/009695399/basedefs/sys/utsname.h.html) as the structure returned by the `uname` function. [The `uname` function](http://pubs.opengroup.org/onlinepubs/009695399/functions/uname.html) returns information about the current system.
    
    The identifier `systemInfo` is just a variable name. It has no special meaning.
    
2. The “need to convert” exists because `utsname.machine` contains a string intended for programs, programmers and technicians, not end users. There have been multiple hardware versions of certain devices, like the iPhone 5S. Apple calls all of them “iPhone 5S” when speaking to users. Internally, you can tell which hardware version you're on by looking at the `utsname.machine` string. If you want to refer to the user's device by its user-friendly name, you need to convert from the `utsname.machine` string to the user-friendly name.


## References 

[SO | detect-current-device-with-ui-user-interface-idiom-in-swift](https://stackoverflow.com/questions/24059327/detect-current-device-with-ui-user-interface-idiom-in-swift)

[apple dev | uikit/uidevices](https://developer.apple.com/documentation/uikit/uidevices)

[apple doc official](https://developer.apple.com/documentation/xcode/running-code-on-a-specific-version/)