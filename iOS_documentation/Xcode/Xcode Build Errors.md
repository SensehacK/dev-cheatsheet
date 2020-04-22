# Xcode Build Errors


## Couldn’t find path for xcconfig pods

-     Set the configuration file setting* "None" for the Pods related target.
-     Close the .xcworkspace.
-     Run pod install again
-     now open and build your .xcworkspace

[SO source](https://stackoverflow.com/questions/27109476/incorrect-path-for-pods-debug-xcconfig-in-xcode)


## Build input file cannot be found

Most probably you have changed the root “Info.plist” file and due to that Xcode haven’t updated its default move location in the Build Settings.

[SO Fix Link](https://stackoverflow.com/questions/52435202/build-input-file-cannot-be-found-swift-4-2-xcode-10-0)





