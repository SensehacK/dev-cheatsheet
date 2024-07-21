# Swift Package Manager

## Intro

Versatile yet out of beta package manager. Great support in built in Xcode IDE. 
Still initial adoption pain back in 2020, 2021. I think so past two years it has matured quite a bit.

## Setup

You can utilized the Xcode SPM functionality in built with version 11

Great for linking different packages and frameworks to Xcode with first class support.

No messy `.xcodeproj` / `.xcworkspace` file

Create 

```sh
swift package 
```
[apple docs | swift package - create a standalone package xcode](https://developer.apple.com/documentation/xcode/creating-a-standalone-swift-package-with-xcode)


## Sample Package.swift


```swift
let package = Package(
    name: "test-apple",
    platforms: [
        .iOS(.v16),
        .tvOS(.v16)
    ],
    products: [
		.library(
            name: "DummyUnit",
            targets: ["DummyUnit"]),
    ],
	dependencies: [
        .package(url: "git@github.com:repo_name/test.git",
        branch: "important-events")
    ],
    targets: [
	    .target(
            name: "DummyUnit",
            dependencies: [],
            path: "Sources/product_path"
        ),
    ]
)
```

## Directory

### Delete local build cache

If you want to delete the cache via CLI

```sh
swift package purge-cache
```

Note - this command is only applicable from the `$pwd` where there is a `Package.swift` file present.

### Package.resolved file

If it's a traditional `.xcodeProj` we don't have the Package.swift / .resolved file either. It is hidden under the project file. You can right click and browse its contents, below is the location of it.

```location
.xcodeproj/project.xcworkspace/xcshareddata/swiftpm/Package.resolved
```


## Options

### Resolve Package Versions

This tries to take latest pull - origin kind of methodology. So if `9.3.3` tag had been published before with hash ending at `352EA` and now the remote server deleted it and again push few commits and tagged it `9.3.3` it will have the latest commit with new hash like `231EB`. Usually its recommended to not do this kind of tagging or releasing & just follow SemVer but sometimes you can't choose the cross team you're working with. 

Digress: I wish I could be picky enough like Linus Torvalds, only liking to work with people I respect.

### Reset Package Cache

This basically does a soft nuke of the cache and tries to pull it again if the package already had cache setup.

### Update Package versions

This command will update the package depending on the ruleset defined in SPM with Semantic Versioning `Major.Minor.Patch` 
So `9.3.3` has minor versions allowed in update rules could update to `9.x.x`

## Cache

### SwiftPM cache

Cache directory for SPM

```location
~/Library/Caches/org.swift.swiftpm/
```

[Install size](https://forums.swift.org/t/shrinking-toolchain-install-size/44771)
These store the actual repositories of downloaded or cloned dependencies.

### SwiftPM Metadata

This location stores the Repositories resolved meta data. You need to delete the meta data if some repository made a change on the same tag and couldn't even follow `Semantic Versioning` to make sure that the new change isn't propagated everywhere which makes / breaks the whole dependency chain.

```location
~/Library/org.swift.swiftpm/security/fingerprints
```

[swift pm | ReleaseNotes/5.4.md#package-dependency-caching](https://github.com/apple/swift-package-manager/blob/main/Documentation/ReleaseNotes/5.4.md#package-dependency-caching)

## Delete Cache

Full Swift Package manager cache directory

```swift
rm -rf ~/Library/Caches/org.swift.swiftpm
rm -rf ~/Library/org.swift.swiftpm
```

Or a single repository cache

To reset the cache for a single package:

- Navigate to ~/Library/Caches/org.swift.swiftpm/repositories and deleting the folder and lock file related to the package
- Then, in Xcode, run File-->Swift Packages-->Reset Package Caches


```
## Dependency

Adding a branch as a dependency or a tag.

```swift
dependencies: [
	.package(url: "git@github.com:company-player/dracula.git", branch: "br-logging"), 
	 .package(url: "git@github.com:company-player/dracula.git", exact: "0.3.0"),
]
```

[Similar SPM | Xcode cache issue](ios/xcode/spm_errors#skipping%20cache)

## Bundling

A note with Swift package manager bundling directories.

Swift Package Manager world, bundling basically boils down to the following:

-   `Bundle.module` returns the bundle relative to the call site. so if you call that in `FrameworkCore/AppInfo.swift` it will return the `FrameworkCore` bundle since that file and type are associated with that bundle. if you call it in `FrameworkCoreTestKit/Mock.swift` it will return the test kit bundle since that's where that file lives. so on and so forth
-   if you call `Bundle.main`, that will return the "product" or the bundle containing the current executable. you generally don't want to call this anymore unless you know you want the app layer bundle

## Fetching latest

You have a dependency pointed to specific branch and you push some commits on the dependency's branch. But Xcode and SPM would always use the `cache` version of that dependency. Since we didn't go for `SemVer` approach and just a branch SPM and xcode isn't smart enough to automatically pull in latest or fetch origin. Unless you nuke the cache and SPM manifest metadata with git commits for every package dependency located in `~/Library` directory.

You can avoid that hassle by just updating your packages and invalidating previous cache and Xcode / SPM is smart enough to abide by those Semver rules or just update to the latest commit on the specified branch. 
Note: Manually selecting the library and right clicking to select option `Update` doesn't update it for me Xcode 15 beta 6 with package dependency defined using a `branch: "branch_name"`

### Updating all packages

You can do update by following this option in the menu bar.

```sh
Xcode ->  File -> 
Packages ->
Update to Latest Package versions
```

### Updating individual package

You can also update a specific version on a package dependency by right clicking on it and updating specifically.

## Cross Platform

```swift
// Package.swift
#if !os(Windows)

dependencies.append(.package(url: "https://github.com/danger/swift.git", from: "3.12.1"))

targets.append(.target(name: "DangerDeps", dependencies: [.product(name: "Danger", package: "swift")]))

products.append(.library(name: "DangerDeps", type: .dynamic, targets: ["DangerDeps"]))

#endif
```

[platform-specific-code-in-swift-packages](https://www.polpiella.dev/platform-specific-code-in-swift-packages)

## Migrating to SPM

[migrating-to-spm-from-mix-of-embedded-frameworks-and-static-libraries](https://forums.swift.org/t/migrating-to-spm-from-mix-of-embedded-frameworks-and-static-libraries/34253)

[spm-ifying-yapdatabase](https://www.vanille.de/blog/2020-spmifying-yapdatabase/)



## [SPM Errors](spm_errors.md)

## Notes

Xcode should be quit before deleting the references and cache of SPM. Since Xcode reactively tries to resolve those dependency midway while you're trying to resolve it manually.

Sometimes regenerating your SSH keys on your dev machine is helpful to isolate that permission issues, but since Xcode 14.1, it has been bubbling up better errors to the developer to show what failed and what went wrong. 

This [script from a stackoverflow](https://stackoverflow.com/a/74130700) user also goes through selectively deleting cache from Derived Data and SPM cache manifest files which is more efficient than nuking the whole cache as its more time consuming and resource intensive.
Relevant thread which is tracked on [swift forum](https://forums.swift.org/t/adding-a-swift-package-using-the-ssh-url/60888/19)

## Exposing Library & Target

When working with Swift Package managers you need to expose every folder as a different library in order to import them in the project itself. Swift Packages treat every directory or folder independent and you can't just directly access them if they are out of the default scope of `Package_Name -> Sources` library package name.

```swift
products: [
	.library(
		name: "DummyUnit",
		targets: ["DummyUnit"]),
],
targets: [
	.target(
		name: "DummyUnit",
		dependencies: [.product(name: "testLib", 
								package: "product_name")],
		path: "Sources/product_path"
	),
]
```

In order to access the directory as a library in your codebase, you would have to add dependencies if they are seperate repositories. 

To import just use the following syntax as long as the library builds correctly and is embedded into the project product target in `General Settings` -> `Frameworks, libraries and Embedded Content`

```swift
import DummyUnit
```

For more information on Frameworks refer my [mind map docs](ios/library/framework.md)

## Local Package dependency

You can point a swift package to local option in order to do faster prototyping instead of waiting for xcode to close / fetch / resolve SPM package directory and then make it usable to edit a file. 

+1 Less `.xcodeproj` `xcworkspace` headaches.

Local dependency path in `package.swift` url takes both local and remote paths in its initializer.

```swift
dependencies: [
// Local Package
	.package(url: "/Users/ksave/git/cloud/packageName", branch: "28-events")
	.package(url: "file:///Users/ksave/git/cloud/packageName", from: "6.6.6")

// Remote package
    .package(url: "git@github.com:companyName/packageName.git", branch: "21-events")
],
```

Change set in `.resolved` file 

```git
"identity" : "dependency_name",
- "kind" : "remoteSourceControl",
- "location" : "git@github.com:org-name/dependency_name.git",
+ "kind" : "localSourceControl",
+ "location" : "/Users/username/git/cloud/dependency_name",
```

Sometimes it gives out an error or warning as follows if you have both local dependency and cloud dependency added as a package in Swift PM.

```log
'project-parent-package-name' dependency on 'git@github.com:source/package_name_3.git' conflicts with dependency on '/Users/userName/git/cloud/package_name_3' which has the same identity 'package_name_3'. this will be escalated to an error in future versions of SwiftPM.
```

Add `local` SPM package doesn't work in Pure `Package.swift` project opened in Xcode 16 beta 3. But I could add `local` package in `.xcworkspace` or `.xcproj` file.

Another thing 
For some reason my local package gets added via `Package.swift` with absolute URL local path and still doesn't reflect the right change-set. But if I add it via add package -> local GUI option on a `.xcodeproj` file in Xcode GUI `Package Dependencies` It reflects the local change-set appropriately. Maybe a cache issue? Don't know and don't want to bother learning more about it.
### [An unknown error not found (-1) issue](ios/xcode/spm_errors#skipping%20cache) 


## Pitfalls

[Some pitfalls of using SPM and Build Configuration in Xcode](https://www.sobyte.net/post/2022-10/spm-in-xcode/)

### Unexpected Duplicate tasks

Multiple commands produce `framework` libraries. Probably deleting SPM cache and metadata. also `.resolved` SPM project helps me to get over this build error. Reset Package graph and Resolve Packages as well.

## Circular dependency

Also experienced it in [Carthage build command](ios/xcode/carthage#Dependency%20graph%20cycle)

[SO resolve circular dependency swift PM](https://stackoverflow.com/questions/47872419/resolve-circular-dependency-in-swift)
[swift forums circular dependency](https://forums.swift.org/t/circular-dependencies-in-swiftpm/13580)

[SO | resolve circular dependency](https://stackoverflow.com/questions/47872419/resolve-circular-dependency-in-swift)

Best option is to refactor the code or move dependency one way rather than two ways. Or move it to third package and adopt one way dependencies on both `A` & `B` dependencies.

## Timeline

Supporting Binary dependencies in SPM 
[Added in Swift 5.3](https://github.com/apple/swift-evolution/blob/main/proposals/0272-swiftpm-binary-dependencies.md)
So [carthage](carthage.md) and [cocoapods](cocoapods.md) were used in lot of projects if your dependencies had images, data files, close source code, binaries.

## Resources

[SPM Basics](https://medium.com/server-side-swift-and-more/swift-package-manager-basics-c653de716e13)

https://www.youtube.com/watch?v=QmBZ9wJguS4

[Caching and Purge caching](https://blog.eidinger.info/swift-package-purge-cache)

[SwiftPM: Same sources, multiple targets](https://forums.swift.org/t/swiftpm-same-sources-multiple-targets/48810)

[Deleting cache SO post](https://stackoverflow.com/questions/60033082/how-can-i-reset-the-package-cache-on-just-one-package-with-swift-package-manager)
