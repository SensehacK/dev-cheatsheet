

## Plugins

Add Kotlin multi platform plugin from android studio settings.
After installing, restart the IDE.

## Xcode

Interop between Xcode and Kotlin, via an open source plugin.
Ref [touchlab | xcodeKotlin](https://touchlab.co/xcodekotlin)

```sh
brew install xcode-kotlin
xcode-kotlin install
```

## Configuration

Add the `iOS App` configuration, to directly run the kotlin multi - platform app from Android studio.
Make sure you provide the right `.xcodeproj` directory in the iOS app directory with right scheme selected.


## Errors

### Java runtime not installed

Install java via homebrew - openJDK.
Make sure they are symlink and the path is added to your appropriate profile file like `bashrc` or `zshrc`.
