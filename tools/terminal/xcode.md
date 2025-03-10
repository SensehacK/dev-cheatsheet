# Xcode

## Xcode
### Checking Xcode SDK Path

Will check whether SDK is linked with path. Command Line tools should be installed and symlinked with path.

```sh
xcrun -k --sdk iphoneos --show-sdk-path
```

### Installing Command Line tools

This command would install the Command line tools on the machine.

```sh
xcrun -k --sdk iphoneos --show-sdk-path
```

### Multiple Xcode Developer tools

If you have multiple versions of the Apple developer tools installed (an Xcode beta, for example), use `xcode-select` to change which version xcode or other build tool uses.

Show which xcode path is being used in Command Line Tools.

```sh
xcode-select -p
```


### Switch Xcodes

#### GUI
 
 `Xcode -> Preferences -> Locations`

#### CLI

You should be pointing it towards the `Developer` directory, not the Xcode application bundle. 

```swift
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
```

## Swift

### Check Swift Version

```sh
xcrun swift -version

## Output
swift-driver version: 1.90.11.1 Apple Swift version 5.10 (swiftlang-5.10.0.13 clang-1500.3.9.4)
Target: x86_64-apple-macosx14.0
```

You can check it in Xcode project GUI as well.
Select Target -> Build Settings -> Search `Swift Language Version`
