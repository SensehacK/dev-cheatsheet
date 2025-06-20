# Carthage
## Intro

Carthage’s focus is to share dynamic frameworks. Dynamic frameworks are a superset of Swift packages.

## Installation

Download the installer from [github repo](https://github.com/Carthage/Carthage)

Check if Carthage is installed on your machine by running this command 

```sh
carthage version
```

## Update

Use  command 

```sh
brew upgrade carthage
```
If the above doesn't work, that means you have not installed carthage using Homebrew.


In my case it is _**"/usr/local/bin/carthage"**_.

If you have installed through .pkg then Use these commands to delete every trace of carthage

```sh
## It will show the current path of carthage  
which carthage

## Delete packages
rm -rf /usr/local/bin/carthage

sudo rm -rf /Library/Frameworks/CarthageKit.framework

## Install fresh carthage  
brew install carthage
```

## Getting Started

- Create [cartfile](https://github.com/Carthage/Carthage/blob/master/Documentation/Artifacts.md#cartfile) as describe in the github link.

- After that run carthage update command 

```sh
carthage update --use-xcframeworks
```

Platform specific steps for getting frameworks to be build and appropriately linked is here for [iOS](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) 

### Working

Carthage leaves the linking part to end user and just generate the frameworks or libraries. It makes sure that it gets cloned and build. After that the developer can have scripts which can do copy commands to get all the dependencies to the appropriate folder in `Xcode_project_name_folder/Frameworks`

## Locations

Carthage stores its checkouts and builds in the current project it is building. 
So `ProjectName/Carthage/`

Fetching will be downloaded in [Carthage/Checkouts](https://github.com/Carthage/Carthage/blob/master/Documentation/Artifacts.md#carthagecheckouts) first and then it will try to build or compile to this folder [Carthage/Build](https://github.com/Carthage/Carthage/blob/master/Documentation/Artifacts.md#carthagebuild) 

## Note

I do believe that the community has moved away from Carthage in general to either Cocoapods or Swift Package manager.


## Syntax

Setting the right branch or tag

```sh
# branch
github "https://github.com/org/repo_name.git" "branch_develop"

# tags
github "https://github.com/org/repo_name.git" == 0.6.9
" " ~> 3.453.
```

## Debugging

Sometimes it is helpful to just open the generated Carthage log file and sift through the errors of what went wrong and where. Also opening the `checkout` directory and manually opening it with Xcode with your dependency could help to isolate the build failed errors.


```sh
carthage update --verbose
```

## Updating

For a Cartfile like the following
```cartfile
github "Alamofire/Alamofire"
github "ReactiveX/RxSwift"

# CPlatform
github "https://github.com/company-org/cplatform_ios.git" "branchName"
```

You could choose to update one dependency

```sh
carthage update Alamofire
carthage update cplatform_ios
```

[SO | carthage individual update](https://stackoverflow.com/a/36421394/5177704)


## Checkout 

I found an interesting tidbit with Carthage - thought I would share. If you don't provide a tag or a branch it takes the highest version of tag in the project. 
Now our project for some reason has a tag named `2424.0.32`

## Errors

### shell task failed with exit code 1

```sh
A shell task (/usr/bin/env git fetch --prune --quiet [https://github.com/ephread/Instructions.git](https://github.com/ephread/Instructions.git) refs/tags/_:refs/tags/_ +refs/heads/_:refs/heads/_ (launched in /Users/GALSIV/Library/Caches/org.carthage.CarthageKit/dependencies/Instructions)) failed with exit code 1
```

Just clear the Carthage cache 

```sh
rm -rf ~/Library/Caches/org.carthage.CarthageKit
```

[carthage github forum](https://github.com/Carthage/Carthage/issues/443)

[Reachability github forum](https://github.com/ashleymills/Reachability.swift/issues/340#issuecomment-515991724)


### xcodebuild timed out

```sh
*** Invalid cache found for project_ios, rebuilding with all downstream dependencies
*** Building scheme "Project" in Project.xcodeproj
xcodebuild timed out while trying to read Project.xcodeproj 😭
*** failed to bootstrap Carthage dependencies ***
```

Fixed by opening checked out project, and waiting for successful dependency downloading.  Or maybe open the dependency location in terminal.
Use this command to resolve package dependencies

```sh
xcodebuild -resolvePackageDependencies
```

After that `carthage build projectName-dependency --no-use-binaries --platform iOS` works fine

Or [Stack Overflow recommended post](https://stackoverflow.com/questions/46072080/carthage-xcode-9-xcodebuild-timed-out-while-trying-to-read-xcodeproj-error)

To sort it out I did the following steps:

- Open the timed out project in Xcode
- Do not do anything
- Run `carthage build --platform iOS`
- You can restart macOS as well

Everything compiled without any errors. It seams that once the project is opened in Xcode, Xcode is automatically adding something that is missing and the project compiles then.

This process has to be followed after every "Carthage update", as the update will download a fresh Xcode project.

Note: Make sure your VPN is turned on since one of the few dependencies needed VPN to download it and it wasn't able to connect it within time hence we used to get this error on terminal CLI.


[Github | realm-swift thread](https://github.com/realm/realm-swift/issues/6549)

[Github | facebook-iOS-sdk thread](https://github.com/facebook/facebook-ios-sdk/issues/1251)

[Github | oneSignal thread](https://github.com/OneSignal/OneSignal-iOS-SDK/issues/886)

[Github | Carthage thread | timeout](https://github.com/Carthage/Carthage/issues/3148)



### Deployment target mismatch

This isn't Carthage specific error so you can refer my [xcode build doc -> Errors ](/ios/xcode/build#deployment%20target%20mismatch) for solution.

### Task failed with exit code 65

```sh
*** Building scheme "ProjectDependency_one" in ProjectDependency_one.xcodeproj
Build Failed
	Task failed with exit code 65:
	/usr/bin/xcrun xcodebuild -project /Users/username/code/Project/Carthage/Checkouts/projectName_ios_dependency_one/ProjectDependency_one.xcodeproj -scheme ProjectDependency_one -configuration Release -derivedDataPath /Users/username/Library/Caches/org.carthage.CarthageKit/DerivedData/14.3.1_14E300c/projectName_ios_dependency_one/3.0.0 -sdk iphonesimulator -destination platform=iOS\ Simulator,id=4631D -destination-timeout 3 ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO CODE_SIGN_IDENTITY= CARTHAGE=YES build VALIDATE_WORKSPACE=NO (launched in /Users/username/code/Project/Carthage/Checkouts/projectName_ios_dependency_one)

This usually indicates that project itself failed to compile. Please check the xcodebuild log for more details: /var/folders/1r/njjww2dj6l30hs0sh1fw5phr0000gp/T/carthage-xcodebuild.gvCt62.log
```

Just opening the project manually on Xcode IDE and doing a clean build, checking out `Report Navigator` in the left sidebar. See the build logs and do a `Product` -> `Build` from there. If the build succeeds continue again with your Carthage cli command. 

```sh
carthage build projectName-dependency --platform iOS
carthage bootstrap
```


### Invalid cache found for

Cache issues [thread](https://github.com/Carthage/Carthage/issues/2892)

```sh
xcodebuild: error: Could not resolve package dependencies:
  Failed to clone repository https://github.com/player/Support:
    Cloning into bare repository '/Users//Library/Developer/Xcode/DerivedData/-caujyctqkqefpcbzilmfqapyzsdr/SourcePackages/repositories/-82566464'...
    remote: Repository not found.
    fatal: repository
```

Was able to solve this by opening the xcode -> carthage -> Checkouts directory and building the specific library manually on xcode gui. Close xcode and then try the carthage build command.

Similar thread in [xcode errors](git/errors#remote_repository_not_found)


### explicit build specific framework


Just delete the framework `Carthage` -> `Build` folder  or else by default carthage command will just see if there's any cache build in your WIP project.


```sh
*** Invalid cache found for platform_ios, rebuilding with all downstream dependencies
```

### swift binary mismatch

Read this article in order to make sure that the swift binary is being appropriately set before running `carthage bootstrap` command
[Swift binary framework download compatibility](https://github.com/Carthage/Carthage#swift-binary-framework-download-compatibility)

### Dependency graph cycle

```log
The dependency graph contained a cycle:
yajl:
DIMHAL: FapDatabase
PromiseKit:
securityClient-ios-binary: PromiseKit, yajl, SMobileConfig, 
```

Removing the dependency or contacting them to remove specific dependency is helpful in order to remove circular dependency graph cycle issues.


### Carthage: no shared framework schemes for iOS platform (for my own framework)

Make sure that `.xcodeproj/xcshareddata/xcschemes` is added and pushed to github.

[SO | carthage shared framework scheme](https://stackoverflow.com/questions/35054788/carthage-no-shared-framework-schemes-for-ios-platform-for-my-own-framework)

### command not found

```text
carthage: command not found
```

this is prolly due to conflict with `bash, zsh or ohmyZsh` configs.
You need to update your `.zshrc` file and reload the config / terminal again to get it working.

[Shell zsh PATH fix](tools/terminal/shell#zsh%20issues)



### could not find module

```sh
<unknown>:0: error: could not find module 'OHHTTPStubs' for target 'x86_64-apple-ios-simulator'; found: arm64-apple-ios, at: /Users/kay/git/cloud/slayer/Carthage/Build/OHHTTPStubs.xcframework/ios-arm64/OHHTTPStubs.framework/Modules/OHHTTPStubs.swiftmodule
```


```sh
Task failed with exit code 1
/usr/bin/xcrun dsymutil /Users/kay/Library/Caches/org.carthage.CarthageKit/DerivedData/
...
Framework/BuildProductsPath/Release-appletvos/OHHTTPStubs.framework.dSYM


This usually indicates that project itself failed to compile. Please check the xcodebuild log for more details: /var/folders/.log
```

Upgrading to new carthage solved the issue - miraculously.
[Git diff carthage](https://github.com/Carthage/Carthage/compare/0.39.0...0.40.0) upgrade from `0.39` to `0.40`



## Build local frameworks

Update the project dependency to a `file:///`

Cartfile config example
```sh

# Old
# remote
github "https://github.com/player/platform_.git" == 10.9.1


# New
# local
git "file:///Users/k7/git/cloud/platform_directory" "branch_name_local_integration_client" 
```

Carthage build system will only take committed files to the latest git checkout ref sha code. You can see that in `Cartfile.resolved`


```sh
git "file:///Users/k7/git/cloud/platform_" "b149789dd3b0545e7323422124wac"
```

Note: You need to commit your WIP files, it didn't work with "UnStaged" files in git. Uncommitted changes will not be built.

Please note that `file:/` is used for local files which is useful for developing/debugging dependency. Do not forget to commit changes before using git

Before checking for changed code, you need to commit them.
Delete three files

```sh
Cartfile.resolved
Project_name in  -> Carthage/Build 
Project_name in  -> Carthage/Checkout
~/Library/Caches/org.carthage.CarthageKit
```


[Carthage cartfile example](https://github.com/Carthage/Carthage/blob/master/Documentation/Artifacts.md#example-cartfile)


Binary framework stuff

```
binary "https://my.domain.com/release/MyFramework.json"   // Remote Hosted
binary "file:///some/Path/MyFramework.json"               // Locally hosted at file path
binary "relative/path/MyFramework.json"                   // Locally hosted at relative path to CWD
binary "/absolute/path/MyFramework.json"                  // Locally hosted at absolute path
```
[Carthage github doc](https://github.com/Carthage/Carthage/blob/master/Documentation/Artifacts.md#binary-only-frameworks)

XCworkspace work in the project

[SO | framework dev in carthage](https://stackoverflow.com/questions/38862464/debugging-owned-framework-when-using-carthage)


### No Info plist

```sh
error: There is no Info.plist found at '/Users/git/cloud/platform_ios/Carthage/Build/PP1.xcframework/Info.plist'. (in target 'Platform' from project 'Platform')
error: There is no Info.plist found at '/Users/git/cloud/platform_ios/Carthage/Build/PP2.xcframework/Info.plist'. (in target 'Platform' from project 'Platform')


There is no Info.plist found at '/Users/git/cloud/platform_ios/Carthage/Build/PP1.xcframework/Info.plist'.

There is no Info.plist found at '/Users/git/cloud/platform_ios/Carthage/Build/PP2.xcframework/Info.plist'.
```

This happens due to changing branches with totally different versions of the dependencies, this won't be an issue sometimes since you may have old cache.

If I change to a diff branch and the cache is not there - i will have to run the dreaded command again to relink everything and build appropriately.

```sh
./carthage.sh bootstrap --use-ssh --use-xcframeworks --cache-builds --platform iOS,tvOS --new-resolver
```

## Cache 


```sh
Build description signature: 514999d2f91654983953dd9633cf8ed5
Build description path: /Users/k/Library/Caches/org.carthage.CarthageKit/DerivedData/15.3_15E204a/platform_ios/3305.0.500/Build/Intermediates.noindex/ArchiveIntermediates/Platform/IntermediateBuildFilesPath/XCBuildData/514999d2f.xcbuilddata
/Users/ksave957/git/cloud/XTV/Carthage/Checkouts/playerplatform_ios/Platform.xcodeproj: warning: The iOS deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 8.0, but the range of supported deployment target versions is 12.0 to 17.4.99. (in target 'Platform' from project 'Platform')
warning: Run script build phase 'Run Script' will be run during every build because it does not specify any outputs. To address this warning, either add output dependencies to the script phase, or configure it to run in every build by unchecking "Based on dependency analysis" in the script phase. (in target 'Platform' from project 'Platform')
error: Value for SWIFT_VERSION cannot be empty. (in target 'Platform' from project 'Platform')
** ARCHIVE FAILED **
```



## Resources

[7 Carthage Terminal Commands to Bookmark](https://medium.com/remote-ios-dev/7-carthage-terminal-commands-to-bookmark-6c19b6d16379)

[Carthage Tutorial: Getting Started](https://www.kodeco.com/7649117-carthage-tutorial-getting-started)

[Carthage Cheatsheet](https://kapeli.com/cheat_sheets/Carthage.docset/Contents/Resources/Documents/index)