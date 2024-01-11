# Build Errors

## Basic Remediation

> Have you tried turning it OFF and ON again - The IT Crowd

Glad I can reference that british TV show in my work - hobby - mind map knowledge base.

The number of times an iOS Engineer has to go back to basics things to try while having a build or runtime error from Xcode - Apple Developer Tools.

- Manually clearing out Derived Data
- Clean Build Folder
- Deleting app on simulator
- Closing Xcode
- Force quitting Xcode
- Swift Package Manager - Reset package cache
- SPM - resolving packages
- Restarting Mac



## Finding the culprit

Open the `.log` file on `console.app` and make sure to not take the last error stack trace at its face value. 
Always back track to a point where you can see the actual error.
When Xcode build command fails on GUI or CLI. CLI is a little bit tricky and can only provide final failure information of below logs. 

```sh
** BUILD FAILED **
** ARCHIVE FAILED **
```

You can solve this problem two ways 

1. Open the file / error project target scheme product file in question on Xcode GUI. After Xcode 14 updates, lots of debug build logs are available in verbose in GUI rather than just a `.log` file.
2. Or open the log file and search for `error` or `errors generated.` or `error generated.` in your log file. This will give you which file is failing on CLI.

Usually it happens due to multiple different Xcode versions on GUI and `xcode-select` path set for CLI.
So it comes down to a making sure that whatever tool you're using is on same versions either GUI or CLI. And sometimes `hotfixes` or `build-fixes` are merged in latest `develop` , `main` or `tag` so make sure the branch you're working on is also updated with latest merges from parent branches or protected branches.

Or else you can face a classic `It Works on my machine!` or `Multiple Spiderman pointing at each other` meme IRL.

## Couldn’t find path for `xcconfig` pods

* Set the configuration file setting\* "None" for the Pods related target.
* Close the `.xcworkspace`
* Run pod install again
* now open and build your `.xcworkspace`

[SO source | incorrect path for pods](https://stackoverflow.com/questions/27109476/incorrect-path-for-pods-debug-xcconfig-in-xcode)

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


```sh
error: module name "" is not a valid identifier 
```

[medium | xcode-10-xcode-11-2-x-error-multiple-commands-produce](https://medium.com/codespace69/xcode-10-xcode-11-2-x-error-multiple-commands-produce-4e5ab75558f2)


SWIFT\_ENABLE\_BATCH\_MODE 
[SO | build-fails-with-command-failed-with-a-nonzero-exit-code](https://stackoverflow.com/questions/46690619/build-fails-with-command-failed-with-a-nonzero-exit-code)

## Failed to set plugin placeholders

[SO | failed to set placeholders](https://stackoverflow.com/questions/47344160/failed-to-set-plugin-placeholders-message)

## Invalid code signature

```sh
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

```sh
Showing Recent Messages
/Users/ksave/Automation/Projects/Pods/Target Support Files/Pods-API/Pods-API.debug.xcconfig: unable to open file (in target "API" in project "API")

```

Maybe update the proper references and also clear the Derived Data.


## Undefined symbol $_XCTestSwiftSupport

```sh
Undefined symbol: __swift_FORCE_LOAD_$_XCTestSwiftSupport
```

Had to turn this setting on in order to build appropriately.

```sh
PROJECT -> Build Settings -> Build Options -> Enable Testing Search Paths
```
 [XCode 13.1: Undefined symbol: __swift_FORCE_LOAD_$_XCTestSwiftSupport](https://stackoverflow.com/questions/69893836/xcode-13-1-undefined-symbol-swift-force-load-xctestswiftsupport)


## Other Swift Flags

remark: Incremental compilation has been disabled: it is not compatible with whole module optimization

```sh
error: unexpected input file: /Users/ksave/Projects/Project-iOS/RELEASE
```


Command CompileSwiftSources failed with a nonzero exit code
By removing that flag it was able to compile again but I can change the Swift Compiler mode according to this thread on [SO](https://stackoverflow.com/questions/68801998/remark-incremental-compilation-has-been-disabled-it-is-not-compatible-with-who)



 ## debugserver is x86_64 binary running in translation, attached failed
 
 Faced it in Xcode Playgrounds, turns out it was a translation issue related to Rosetta 2 emulation being checked by default. Disabling that using `Xcode.app` -> Get Info. Unchecking `Open using Rosetta`

https://stackoverflow.com/questions/72796354/debugserver-is-x86-64-binary-running-in-translation-attached-failed-could-not

https://sarunw.com/posts/open-using-rosetta-in-xcode-14-3/


## Platform Path

```sh
swift build -v
error: terminated(1): /usr/bin/xcrun --sdk macosx --show-sdk-platform-path output:
    xcrun: error: unable to lookup item 'PlatformPath' from command line tools installation
```

Just set the xcode default path 

```bash
sudo xcode-select -switch /Applications/Xcode.app
```

## Show Rosetta Build

If you need to have Rosetta simulators in xcode, you can show them in Xcode settings.

Go to “**Product**” in the menu bar and select **Destination -> Destination Architectures -> Show both**

[medium | run-rosetta-simulator-on-xcode-14-3](https://armen-mkrtchian.medium.com/run-rosetta-simulator-on-xcode-14-3-381d341364ee)

### Logic Testing on devices not supported

Make sure the test target with the section of `General` -> `Testing`. 
Enable the `Host Application` with the App target to run the unit tests on physical device.

[SO | logic-testing-on-ios-devices-is-not-supported](https://stackoverflow.com/questions/8454935/logic-testing-on-ios-devices-is-not-supported)

## Xcode  failed to verify module interface of 'project' 

`failed to verify module interface of 'projectName' due to the errors above; the textual interface may be broken by project issues or a compiler bug`  
along with `No such module Firebase`

Enable the flag 
`-no-verify-emitted-module-interface` to Other Swift Flags in Build Settings for SPM dependency issue.

[SO | xcode-14-3-failed-to-verify-module-interface-of-project](https://stackoverflow.com/questions/75929888/xcode-14-3-failed-to-verify-module-interface-of-project)


https://github.com/apple/swift/issues/64669



## deployment target mismatch

```log
/code/Project/Carthage/Checkouts/projectName_ios_dependency_one/ProjectDependency_one.xcodeproj: warning: The iOS Simulator deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 10.2, but the range of supported deployment target versions is 11.0 to 16.4.99. (in target 'ProjectDependency_one' from project 'ProjectDependency_one')
** BUILD FAILED **
```
Just open the project in Xcode and set your `Project.xcodeproj` file with `Targets` selected, `General` Tab and `Minimum Deployments` section to the range required by the project.

## clang error building for iOS simulator

```log
ld: in building for iOS Simulator, but linking in object file built for iOS, file `filePath` for architecture arm64

clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

`BuildSettings -> Search -> "Architectures" -> Build Active Architecture Only` 

Comment copied from [apple dev forums](https://developer.apple.com/forums/thread/657913)
I've seen quite a bit of weird behavior with frameworks, I think due to changes to the simulators to support Apple silicon. My temporary workaround is, in my app/extension targets, to add "arm64" to the Excluded Architectures build setting when building for the simulator (as your preview appears to be trying to do), and setting "Build Active Architecture Only" to No for all schemes. Might be worth a try.

## iOS simulator vs iOS vs iOS Rosetta

```sh
Building for 'iOS-simulator', but linking in object file `filepath` built for 'iOS'

Linker command failed with exit code 1 (use -v to see invocation)
```

Switching to iOS physical device or Rosetta simulator fixed it for us.
Basically you can get away by mentioning the `excluded architecture` in your xcode build command.

## Scheme `name` is not currently configured for the test action.

```log
xcodebuild: error: Scheme TestAppUI is not currently configured for the test action.
```

Two approaches 

- Fix the workspace file so the Package is a dedicated scheme.
- Remove the workspace and .xcodeproj files. As far as I can tell, these are just used to run some UI which we never touch. The source files will still be there so we can add them back in the future if we need them.

Reasons

- They introduce multiple schemes which makes isolating the package target/scheme we want to use difficult with `xcodebuild`
- The source files are being left in the repository. Those workspace/proj files were being used to write "UI" around the code, which is not necessary since we rely on the unit tests for CI

## Carthage linking framework issue

TODO: - Clean this logs before committing to the repo.

```log
ld: warning: ignoring duplicate libraries: '-lc++'
ld: warning: search path '/Users/username/git/cloud/project_ios/lib' not found

ld: warning: search path '/Users/username/git/cloud/project_ios/Carthage/Build/iOS/Static/URITemplate.framework' not found

ld: warning: search path '/Users/username/git/cloud/project_ios/lib' not found

ld: warning: search path '/Users/username/git/cloud/project_ios/Carthage/Build/iOS' not found

ld: warning: Could not find or use auto-linked framework 'CoreAudioTypes': framework 'CoreAudioTypes' not found

ld: Undefined symbols:
  (extension in dependency):Swift.Int.init(string: Swift.String) -> Swift.Int?, referenced from:
      projectTestUI.AssetMetadataViewController.(updateMetadata in _B9498481024380D6BB227EFDF8C66DC5)() -> () in AssetMetadataViewController.o
  (extension in dependency):Swift.Collection.subscript.getter : (safe: A.Index) -> A.Element?, referenced from:
      projectTestUI.AssetTableViewController.tableView(_: __C.UITableView, canEditRowAt: Foundation.IndexPath) -> Swift.Bool in AssetViewController.o
      projectTestUI.AssetTableViewController.tableView(_: __C.UITableView, commit: __C.UITableViewCellEditingStyle, forRowAt: Foundation.IndexPath) -> () in AssetViewController.o
  (extension in dependency):Swift.Collection.indicies(containsIndex: A.Index) -> Swift.Bool, referenced from:
      projectTestUI.CustomAssetStore.remove(at: Swift.Int) -> () in CustomAssetStore.o
  static (extension in dependency):Swift.Int32.defaultdependencyTimeScale.getter : Swift.Int32, referenced from:
      projectTestUI.ResumeViewController.(setResumePositionFrom in _8B01A58AC45D5136CBF90D032D54612A)(textField: __C.UITextField) -> Swift.Bool in ResumeViewController.o
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

This got fixed after linking the other SPM framework dependency which had internal `.c` or `.o` library files I believe.
`https://github.com/company-player/iOSPlayerDepSupport`

check its internal dependency just to verify and then clean up and commit.

## rossetta x86_64 | arm64 arch xcode build issues

For some reason xcode doesn't respect the choices for xcode build command being passed around.
Command in test on Xcode 15.0

```sh
xcodebuild -scheme ProjectTest -destination "platform=iOS Simulator,name=iPhone 15,arch=x86_64" build
```

It was selecting the wrong destination, so for some reason the specification of iPhone 15, platform wasn't working as expected.

[Forums suggest using simulator identifier](https://github.com/fastlane/fastlane/issues/21293#issuecomment-1562332624) to mitigate the destination being respect properly.

```sh
xcodebuild -scheme ProjectTest -destination "platform=iOS Simulator,name=iPhone 15,id=2C265EE3-6572-458F-BBD3-98C0285658B0,arch=x86_64" test
```

or 
hard code the architecture settings to `x86_64` to make sure it only runs it on `Rosetta` simulator on M.x arm64 chips.
After doing that you would be granted as this status on CLI

```sh
Build settings from command line:
    ARCHS = x86_64
```

[Bug thread on xcode toolchain, fastlane github](https://github.com/fastlane/fastlane/issues/21293)

## xcode build log file empty

```sh
open /var/folders/fj/1kwwbqhx5r3d0dp1g1fgjwbw0000gn/T/carthage-xcodebuild.dCp7BC.log -a Console
```

Sometimes the log file being generated by `xcode build` command is empty at first when opened using `Console.app`. Wait for few secs depending on your machine's CPU power and it should populate the logs appropriately. Using other text editor doesn't capture the live rendering or output of the logs so its very crucial to open it using `Console.app` in macOS.
[Carthage github empty log issue](https://github.com/Carthage/Carthage/issues/151)

## CoreSimulator is out of date

```log
The version of the CoreSimulator framework installed on this Mac is out-of-date and not supported by this version of Xcode
```

[Apple Dev forums | Fixing CoreSimulator is out of date](https://developer.apple.com/forums/thread/666924?answerId=648561022)

Make sure when you opened the new Xcode version and were you prompted to "install additional components?" if so, click "install" let it install.
And re-run whatever you were trying to achieve.

Or make it explicit run this command

```sh
sudo xcodebuild -runFirstLaunch
```


## does not contain expected binary artifact

```log
downloaded archive of binary target 'securityFramework' does not contain expected binary artifact named 'securityFramework'
```

In SPM, known issue on xcode 14 | [github thread discussion](https://github.com/kewlbear/Open3D-iOS/issues/38)
resetting package , clean build or again deleting and adding the package

and if that doesn't help you can try deleting the spm cache
 
```sh
rm -rf ~/Library/org.swift.swiftpm 
rm -rf ~/Library/Caches/org.swift.swiftpm/
```


