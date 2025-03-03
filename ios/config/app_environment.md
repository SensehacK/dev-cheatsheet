# App Environment

## Setup
Setting up different configurations for different environments.

Debug
Staging
Production

[Article](https://sarunw.com/posts/how-to-set-up-ios-environments)


## Xcode Build

Lots of flags in Xcode build environment. The following website provides better documentation regarding what each flag does.

[Xcode build settings](https://xcodebuildsettings.com/)

## Feature Flags

Use Swift Compiler - Custom flags option in Xcode Target build settings in order to set some initial checks when launching the app with different environment options or configurations.

```swift
#if DEBUG
	print("In DEBUG mode")
#else
	print("Not in DEBUG mode")
#endif
```

[swiftbysundell |feature-flags-in-swift](https://www.swiftbysundell.com/articles/feature-flags-in-swift/)

[environment_variables](environment_variables.md)

Caveat in Swift Package - custom compilation flag is isn't supported in build configuration for SPM. Xcode 13. SPM only supports two build configs `.debug` and `.release` 
You can read more about it [here](/ios/xcode/spm#Pitfalls)

### Custom compilation conditions

```swift
...
targets: [
  .target(
    name: "MyLibrary",
    dependencies: [],
+   swiftSettings: [.define("CUSTOM", .when(configuration: .debug))]
  ),
...
```