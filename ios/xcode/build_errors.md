# Build Errors

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

## Multiple commands produce


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

[SO | debugserver-is-x86-64-binary-running-in-translation-attached-failed-could-not](https://stackoverflow.com/questions/72796354/debugserver-is-x86-64-binary-running-in-translation-attached-failed-could-not)

[open-using-rosetta-in-xcode-14-3](https://sarunw.com/posts/open-using-rosetta-in-xcode-14-3/)

## Platform Path

```sh
swift build -v
error: terminated(1): /usr/bin/xcrun --sdk macosx --show-sdk-platform-path output:
    xcrun: error: unable to lookup item 'PlatformPath' from command line tools installation
```

Just set the xcode default path 
xcode switch

```bash
sudo xcode-select -switch /Applications/Xcode.app
```

## Show Rosetta Build

If you need to have Rosetta simulators in xcode, you can show them in Xcode settings.

Go to “**Product**” in the menu bar and select **Destination -> Destination Architectures -> Show both**

[medium | run-rosetta-simulator-on-xcode-14-3](https://armen-mkrtchian.medium.com/run-rosetta-simulator-on-xcode-14-3-381d341364ee)

Xcode 16.3, I see it renamed as `Show all Run destinations`

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

[github | swift/issues/64669](https://github.com/apple/swift/issues/64669)

## deployment target mismatch

```log
/code/Project/Carthage/Checkouts/projectName_ios_dependency_one/ProjectDependency_one.xcodeproj: warning: The iOS Simulator deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 10.2, but the range of supported deployment target versions is 11.0 to 16.4.99. (in target 'ProjectDependency_one' from project 'ProjectDependency_one')
** BUILD FAILED **
```
Just open the project in Xcode and set your `Project.xcodeproj` file with `Targets` selected, `General` Tab and `Minimum Deployments` section to the range required by the project.


Make sure you have open in Rosetta mode in terminal. So that carthage can properly link in llvm build commands and build cache appropriately.

## clang error building for iOS simulator

```log
ld: in building for iOS Simulator, but linking in object file built for iOS, file `filePath` for architecture arm64

clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

`BuildSettings -> Search -> "Architectures" -> Build Active Architecture Only` 

Comment copied from [apple dev forums](https://developer.apple.com/forums/thread/657913)
I've seen quite a bit of weird behavior with frameworks, I think due to changes to the simulators to support Apple silicon. My temporary workaround is, in my app/extension targets, to add "arm64" to the Excluded Architectures build setting when building for the simulator (as your preview appears to be trying to do), and setting "Build Active Architecture Only" to No for all schemes. Might be worth a try.
Or if you're on a build script from carthage you could use this 

```sh
function xcconfig_cleanup {
  rm -rf ${TMPDIR}/TemporaryItems/*carthage*
  
  xcconfig=$(mktemp /tmp/static.xcconfig.XXXXXX)
  trap 'rm -f "$xcconfig"' INT TERM HUP EXIT

  # For Xcode 12 make sure EXCLUDED_ARCHS is set to arm architectures otherwise
  # the build will fail on lipo due to duplicate architectures.

  CURRENT_XCODE_VERSION=$(xcodebuild -version | grep "Build version" | cut -d' ' -f3)
  # Write the excluded arch to specific `xcconfig` file
  echo 'EXCLUDED_ARCHS__EFFECTIVE_PLATFORM_SUFFIX_simulator__NATIVE_ARCH_64_BIT_x86_64 = arm64 arm64e armv7 armv7s armv6 armv8' >> $xcconfig
  echo 'EXCLUDED_ARCHS = $(inherited) $(EXCLUDED_ARCHS__EFFECTIVE_PLATFORM_SUFFIX_$(EFFECTIVE_PLATFORM_SUFFIX)__NATIVE_ARCH_64_BIT_$(NATIVE_ARCH_64_BIT))' >> $xcconfig
  # Set the Environment Path with our temp `.xcconfig` file for customized xcode cli build environment.
  export XCODE_XCCONFIG_FILE="$xcconfig"
}
```

[Github Carthage Code link](https://github.com/Carthage/Carthage/issues/3019#issuecomment-665136323)

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

Imp Note: Make sure your terminal or iTerm is running via `Rosetta` mode since carthage & xcode cli had issues in past with getting the `arch` build successfully running on the mac.  [check arch on terminal](/ios/library/framework#Build%20Output)

## xcode build log file empty

```sh
open /var/folders/fj/1kwwbqhx5r3d0dp1g1fgjwbw0000gn/T/carthage-xcodebuild.dCp7BC.log -a Console
```

Sometimes the log file being generated by `xcode build` command is empty at first when opened using `Console.app`. Wait for few secs depending on your machine's CPU power and it should populate the logs appropriately. Using other text editor doesn't capture the live rendering or output of the logs so its very crucial to open it using `Console.app` in macOS.
[Carthage github empty log issue](https://github.com/Carthage/Carthage/issues/151)

Note: Make sure your VPN is turned on since one of the few dependencies needed VPN to download it and it wasn't able to connect it within time hence we used to get this error on terminal CLI and it never moved to actually building the project / product. Hence the `log` file would be empty.
Since in order to have logs you need to first resolve `dependencies` from SPM or static / dynamic libraries.

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

## Tool-hosted testing is unavailable

```sh
Cannot test target “CustomPlatformTests” on “iPhone-JH32GR”: Tool-hosted testing is unavailable on device destinations. Select a host application for the test target, or use a simulator destination instead.
Domain: XCTHTestRunSpecificationErrorDomain
Code: 2
User Info: {
    DVTErrorCreationDateKey = "2024-01-23 17:58:16 +0000";
}
--
```

## launchd_sim: could not bind to session

```sh
Failed to prepare device 'iPhone 15' for impending launch. (Underlying Error: Unable to boot the Simulator. launchd failed to respond. (Underlying Error: Failed to start launchd_sim: could not bind to session, launchd_sim may have crashed or quit responding))
```
Restarted just the test again and it seems it worked after re-running it.


## command SwiftCompile failed with a nonzero exit code

```sh
command SwiftCompile failed with a nonzero exit code
```

Basically saying `The compiler is unable to type-check this expression is reasonable time`


## Build input file cannot be found

```log
error: Build input file cannot be found: '/Users/k/Library/Developer/Xcode/DerivedData/CPlatform-/Build/Products/Debug-iphoneos/CPlatformTestUI.app/PlugIns/CPlatformTests.xctest/CPlatformTests'. Did you forget to declare this file as an output of a script phase or custom build rule which produces it? (in target 'CPlatformTests' from project 'CPlatform')
```

Close simulator which was running force quit it or choose `Rosetta` simulator since if some of the dependencies still rely on `x86` arch then you may not get the right build error thrown out.
Or add `arm64` to Excluded Architectures in Xcode build settings.

Also similar issue could be what [SO user describes here](https://stackoverflow.com/a/73965110/5177704) 
Seems like you have moved bridging file to other folder and Xcode compiler can not find it. Try to move this file in the top of your files tree


## Cannot find type '' in scope

```error
Cannot find type 'CustomNewType' in scope
```

Sometimes you need to have clean build when xcode / swift llvm compiler couldn't resolve its dependencies properly.
This happens when you create a new file in a different namespace or package. SPM which was used for local development imported in an xcode project workspace environment had issues finding a new type defined by me.

So I circumvented this build error by copying the type `struct | protocol` into the same file so that compiler can get the necessary inferences or linking headers / types to unblock myself for now.
After 3 - 4 local builds, I finally moved the type to its own file_name which I tried to do in first place.
No more build errors

## xcodebuild timed out while trying to read

[Carthage issue CLI described here](/ios/xcode/carthage#xcodebuild%20timed%20out)

## Found no destinations for the scheme

```error
xcodebuild: error: Found no destinations for the scheme 'Obs tvOS Framework' and action archive.
```

Just make sure you have the right simulator installed for your Xcode.
For me it happened after Xcode 15.2 -> Xcode 15.3.
So for one of the tvOS framework xcode wasn't backwards compatible? in the UI at least and was showing get `tvOS 17.4`.

## xcode build swiftc unable to discover

```error
error: Unable to discover `swiftc` command line tool info: Could not parse Swift versions from:  (in target 'CoreC' from project 'package-custom')
```

After countless restarts of the CI triggers using Github actions & macOS runner with github, turns out deleting the `builder/actions-runner/_work/package-custom` folder and letting it clone fresh. Solved this issue.
Since running the same command on locally cloned repo was able to generate the build output just fine.

```yml
{% raw %}
env:
	scheme: ${{ 'CoreC' }}
	platform: ${{ 'iOS Simulator' }}
	workspace: ${{ 'package-custom.xcworkspace' }}

run: | 
	device=`xcrun xctrace list devices 2>&1 | grep -oE 'iPhone.*?[^\(]+' | head -1 | awk '{$1=$1;print}' | sed -e "s/ Simulator$//"`
	xcodebuild -workspace "$workspace" -scheme "$scheme" -destination "platform=$platform,name=$device" build
{% endraw %}
```

Shutting down the computer to go outside. Wasted 30 mins to tackle this CI issue.







## Attaching | Installing to Device Loading


Had to restart my device, remove my computer from the device's "trusted" settings and re-install the iOS / mac app.


## Internal inconsistency error


```sh 
**Showing All Messages**
Internal inconsistency error: never received task ended message for task ID '501' with rule info 'SwiftCompile normal x86_64 /Users/saf3/Library/Developer/Xcode/DerivedData/slayer-/SourcePackages/checkouts/hnj/Sources/sa/Utilities/saf/asf.swift'. Build again to continue.
```



## Internal inconsistency error: received multiple target

```log
Internal inconsistency error: received multiple target ended messages for target ID '8' or received target ended message but did not receive corresponding target started message, while retrieving parent activity in taskStarted message.
```

Rebuild the project with Xcode and it worked fine


## ensure you have llvm-symbolizer

```
Stack dump without symbol names (ensure you have llvm-symbolizer in your PATH or set the environment var `LLVM_SYMBOLIZER_PATH` to point to it)"
```

[Link to Github Gist](https://gist.github.com/trevorhobenshield/6bca58f947ad6115a113a97072df1a73)



## entitlement does not match

```log
This application's application-identifier entitlement does not match that of the installed application. These values must match for an upgrade to be allowed.
```

Prolly due to toggling of "Automate manage signing" for your app and deploying that app once on your physical apple device.
And once you discard your WIP stash you revert back to default "manual signing". It kinda led to mismatch provisioning profile or signing package. Which doesn't allows you do perform an upgrade or overwrite the app package.

[SO Post](https://stackoverflow.com/questions/32677133/app-installation-failed-due-to-application-identifier-entitlement)


## Error: missing required module

For me:
This happened due to wrong case in my SPM project target and product.
After I change my typo, I had to delete my old `automatic` generated project scheme and again make sure change the `import module_name` everywhere.

After that it should compile properly? 

[SPM_build_error](/ios/xcode/spm_errors#missing%20required%20module)

[forum - swift discussion](https://forums.swift.org/t/error-missing-required-module-numericsshims/58235)


## Could not find or use auto-linked framework

undefined symbols for architecture

```log
ld: warning: Could not find or use auto-linked framework 'CoreAudioTypes': framework 'CoreAudioTypes' not found
Undefined symbols for architecture x86_64:
  "(extension in CoreCommon):Swift.Comparable.clamped(to: Swift.ClosedRange<A>) -> A", referenced from:
      CoreCommonTests.ClampedTests.testLowerLimitOfClampedFunction() -> () in ClampedTests.o
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

This was fixed by providing the `Target` Test or Source with a dependency in SPM manifest file

```swift
# Before
.testTarget(name: "CoreCommonTests")

# After
.testTarget(name: "CoreCommonTests",
            dependencies: ["CoreCommon"])
```


### bundle image is missing

```error
(kAMDMobileImageMounterPersonalizedBundleMissingVariantError: The bundle image is missing the requested variant for this device.)
```

This could be due to your test device being new or your OS version isn't supported yet for Xcode version installed.

This happened for me on Xcode 15.3 & I had to update from Xcode 16.0 beta 6 to 16.2 beta 2.

Restarting & turning off/on developer mode didn't help.


### Internal inconsistency error

```  
Internal inconsistency error: never received target ended message for target ID '1' (in target 'CCommon' from project 'player-apple'). Build again to continue.
```

Just build again & hopefully it should work.


## textual interface broken

Don't know why I'm not able to see this error for my project compilation build. 
Xcode 15.3

```swift
Failed to build module 'project' for importation due to the errors above; the textual interface may be broken by project issues or a compiler bug
```


## this SDK is not supported by the compiler

```
Failed to build module 'PlayerPlatform'; this SDK is not supported by the compiler (the SDK is built with 'Apple Swift version 5.10 (swiftlang-5.10.0.13 clang-1500.3.9.4)', while this compiler is 'Apple Swift version 6.0.3 effective-5.10 (swiftlang-6.0.3.1.4 clang-1600.0.30)'). Please select a toolchain which matches the SDK
```



## never received target ended message

```log
Internal inconsistency error: never received target ended message for target ID '53' (in target 'XTV' from project 'X2'). Build again to continue.
```


## scheme command not found

```sh
xcodebuild: error: The directory /Users/sensehack/git/cloud/dev/ does not contain an Xcode project.

./generate_docs.sh: line 32: -scheme: command not found
```



This fixes by providing `-workspace` to xcodebuild docbuild

```sh
# invoke xcode build to create documentation
xcodebuild docbuild \
-workspace 'Player.xcworkspace' \
-scheme $TARGET_SCHEME \
-derivedDataPath $DERIVED_DATA_PATH \
-destination 'generic/platform=iOS';
```



## module not found

```log
/Users/builder/actions-runner/_work/player-apple/player-apple/Sources/PlayerCore/Events/Models/DeviceConfig.swift:9:8: error: no such module 'PlayerAnalytics'
import PlayerAnalytics
```

This is a package based out of android KMP -> swift package `.xcframework`
Also `PlayerCore` doesn't have this dependency target but this builds fine on Xcode GUI for the project where its a `workspace` which house `SPM project` inside it as well as a `TestUI`
So xcode or llvm build system does some magic on GUI to automagically link those frameworks automatically.

But when we run `xcodebuild` cli, it fails for me.

So the fix was explicitly adding the `.product(name: "PlayerAnalytics"` inside the `package` which is failing on terminal but when I select the scheme `PlayerCore` on xcode gui it works without any errors or compilation errors.


```swift
Pacakge.swift
dependencies: [
	.package(url: "git@github.com:viper-player/zephyr.git", exact: "0.119.0"),
	.package(url: "git@github.com:viper-player/analytics_android", exact: "7.3.3"),
],

targets: [
	target(
		name: "PlayerCore",
		dependencies: [
		    .product(name: "Zephyr", package: "zephyr"),
		    .product(name: "PlayerAnalytics", package: "analytics_android"),
		],
		path: "Sources/PlayerCore",
        plugins: [.plugin(name: "SwiftLintBuildToolPlugin",
					      package: "SwiftLintPlugins")]
		)
]
```

[SO | spm module not found](https://stackoverflow.com/questions/57165778/getting-no-such-module-error-when-importing-a-swift-package-manager-dependency)

This also connects with the next xcode build error as well below `package is required using a stable-version`
## package is required using a stable-version

This started because we had to support flutter team coz they couldn't access github releases artifact `.zip` `.xcframework` deliverable. So we had to move that artifact into the repo and tag it ( i know weird stuff with flutter ) but bare with me, the branch rules work fine on our machines but for some reason their build system craps out on them with this config 

```sh
xcodebuild: error: Could not resolve package dependencies:
  Failed to resolve dependencies Dependencies could not be resolved because package 'player-apple' is required using a stable-version but 'player-apple' depends on an unstable-version package 'analytics_android' and 'video_player_apple' depends on 'player-apple' 0.118.0.
```
