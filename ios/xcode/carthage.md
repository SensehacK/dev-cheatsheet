# Carthage
## Intro

Carthage’s focus is to share dynamic frameworks. Dynamic frameworks are a superset of Swift packages.

## Installation

Download the installer from [github repo](https://github.com/Carthage/Carthage)

Check if Carthage is installed on your machine by running this command 

```sh
carthage version
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

Everything compiled without any errors. It seams that once the project is opened in Xcode, Xcode is automatically adding something that is missing and the project compiles then.

This process has to be followed after every "Carthage update", as the update will download a fresh Xcode project.

Note: Make sure your VPN is turned on since one of the few dependencies needed VPN to download it and it wasn't able to connect it within time hence we used to get this error on terminal CLI.


[Github | realm-swift thread](https://github.com/realm/realm-swift/issues/6549)

[Github | facebook-iOS-sdk thread](https://github.com/facebook/facebook-ios-sdk/issues/1251)

[Github | oneSignal thread](https://github.com/OneSignal/OneSignal-iOS-SDK/issues/886)



### Deployment target mismatch

This isn't Carthage specific error so you can refer my [xcode build doc -> Errors ](ios/xcode/build#deployment%20target%20mismatch) for solution.

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

## Resources

[7 Carthage Terminal Commands to Bookmark](https://medium.com/remote-ios-dev/7-carthage-terminal-commands-to-bookmark-6c19b6d16379)

[Carthage Tutorial: Getting Started](https://www.kodeco.com/7649117-carthage-tutorial-getting-started)

[Carthage Cheatsheet](https://kapeli.com/cheat_sheets/Carthage.docset/Contents/Resources/Documents/index)