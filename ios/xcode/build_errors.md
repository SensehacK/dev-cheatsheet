# Build Errors

## Basic Remidiation

> Have you tried turning it OFF and ON again - The IT Crowd

Glad I can reference that british TV show in my work - hobby - mind map knowledgebase.

The number of times an iOS Engineer has to go back to basics things to try while having a build or runtime error from Xcode - Apple Developer Tools.

- Manually clearing out Derived Data
- Clean Build Folder
- Deleting app on simulator
- Closing Xcode
- Force quitting Xcode
- Swift Package Manager - Reset package cache
- SPM - resolving packages
- Restarting Mac


## Couldn’t find path for xcconfig pods

* Set the configuration file setting\* "None" for the Pods related target.
* Close the .xcworkspace.
* Run pod install again
* now open and build your .xcworkspace

[SO source](https://stackoverflow.com/questions/27109476/incorrect-path-for-pods-debug-xcconfig-in-xcode)

## Build input file cannot be found

Most probably you have changed the root “Info.plist” file and due to that Xcode haven’t updated its default move location in the Build Settings.

[SO Fix Link](https://stackoverflow.com/questions/52435202/build-input-file-cannot-be-found-swift-4-2-xcode-10-0)

## Build Xcode Target membership

Storyboard Target member should be for iOS screen and not watch storyboard.

[Link SO](https://stackoverflow.com/questions/44429415/illegal-configuration-compiling-ib-documents-for-earlier-than-ios-7-is-no-longe)

## Custom Class Can’t link

Whenever your custom class couldn’t be linked in Xcode and it still throws out the error of “Could not find any information for class named Custom Class”

This thing could happen if you have a habit of moving or segregating project files in different folders or changing locations internally. Usually Xcode should update the reference automatically while building or clean build but its a hit or miss. Closing Xcode, cleaning project or deleting derived data didn’t fix the issue for me.

So you should do the following for Xcode to rebuild its index or cache or linking classes / libraries.

```text
    In the project file explorer (left panel) find the class and right click -> Delete
    Remove reference (do not move to trash as you will lose the class for good)
    Right click on the folder that contained the class -> Add files to ...
    Find the class you just deleted in the file system
```

[SO Source Steps](https://stackoverflow.com/questions/17735182/could-not-find-any-information-for-class-named-viewcontroller)

## Invalid Element name

In storyboard and XIB files when there are merge conflicts or git stash conflicts Xcode couldn’t parse the XML data.

You just need to git diff from the files and open in your favorite text editor to accept the stash change or current change. Save it solving the file conflict.

[SO Link](https://stackoverflow.com/questions/21818821/couldnt-open-xib-file-after-git-pull-invalid-element-name)

## Error: Multiple commands produce

[https://medium.com/codespace69/xcode-10-xcode-11-2-x-error-multiple-commands-produce-4e5ab75558f2](https://medium.com/codespace69/xcode-10-xcode-11-2-x-error-multiple-commands-produce-4e5ab75558f2)

error: module name "" is not a valid identifier 

SWIFT\_ENABLE\_BATCH\_MODE [https://stackoverflow.com/questions/46690619/build-fails-with-command-failed-with-a-nonzero-exit-code](https://stackoverflow.com/questions/46690619/build-fails-with-command-failed-with-a-nonzero-exit-code)

## Failed to set plugin placeholders

[Stack Overflow](https://stackoverflow.com/questions/47344160/failed-to-set-plugin-placeholders-message)

## Invalid code signature


```text
Could not launch “HealthSense”
Domain: IDEDebugSessionErrorDomain
Code: 3
Failure Reason: The operation couldn’t be completed. Unable to launch kautilya.HealthSense because it has an invalid code signature, inadequate entitlements or its profile has not been explicitly trusted by the user.
User Info: {
    DVTRadarComponentKey = 855031;
    RawLLDBErrorMessage = "The operation couldn\U2019t be completed. Unable to launch kautilya.HealthSense because it has an invalid code signature, inadequate entitlements or its profile has not been explicitly trusted by the user.";
}
```



## Changing folder name

```
Showing Recent Messages
/Users/ksave/Automation/Projects/Pods/Target Support Files/Pods-API/Pods-API.debug.xcconfig: unable to open file (in target "API" in project "API")

```

Maybe update the proper references and also clear the Derived Data.


## Undefined symbol $_XCTestSwiftSupport

```swift
Undefined symbol: __swift_FORCE_LOAD_$_XCTestSwiftSupport
```

Had to turn this setting on in order to build appropriately.

```swift
PROJECT -> Build Settings -> Build Options -> Enable Testing Search Paths
```
 [XCode 13.1: Undefined symbol: __swift_FORCE_LOAD_$_XCTestSwiftSupport](https://stackoverflow.com/questions/69893836/xcode-13-1-undefined-symbol-swift-force-load-xctestswiftsupport)


## Other Swift Flags

remark: Incremental compilation has been disabled: it is not compatible with whole module optimization

error: unexpected input file: /Users/ksave/Projects/Project-iOS/RELEASE

Command CompileSwiftSources failed with a nonzero exit code
By removing that flag it was able to compile again but I can change the Swift Compiler mode according to this thread on [SO](https://stackoverflow.com/questions/68801998/remark-incremental-compilation-has-been-disabled-it-is-not-compatible-with-who)



 ## debugserver is x86_64 binary running in translation, attached failed
 
 Faced it in Xcode Playgrounds, turns out it was a translation issue related to Rosetta 2 emulation being checked by default. Disabling that using `Xcode.app` -> Get Info. Unchecking `Open using Rosetta`

https://stackoverflow.com/questions/72796354/debugserver-is-x86-64-binary-running-in-translation-attached-failed-could-not