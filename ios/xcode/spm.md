# Swift Package Manager

## Intro

Versatile yet out of beta package manager. Great support in built in Xcode IDE. 
Still initial adoption pain back in 2020, 2021. I think so past two years it has matured quite a bit.





## Setup

You can utilized the Xcode SPM functionality in built with version 11

Great for linking different packages and frameworks to Xcode with first class support.

No messy .xcodeproj / .xcworkspace file

Create 

```sh
swift package 
```

https://developer.apple.com/documentation/xcode/creating-a-standalone-swift-package-with-xcode

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


https://github.com/apple/swift-package-manager/blob/main/Documentation/ReleaseNotes/5.4.md#package-dependency-caching

## Dependency

Adding a branch as a dependency or a tag.

```swift
dependencies: [
	.package(url: "git@github.com:company-player/dracula.git", branch: "br-logging"), 
	 .package(url: "git@github.com:company-player/dracula.git", exact: "0.3.0"),
]
```

## Bundling

A note with Swift package manager bundling directories.

Swift Package Manager world, bundling basically boils down to the following:

-   `Bundle.module` returns the bundle relative to the call site. so if you call that in `FrameworkCore/AppInfo.swift` it will return the `FrameworkCore` bundle since that file and type are associated with that bundle. if you call it in `FrameworkCoreTestKit/Mock.swift` it will return the test kit bundle since that's where that file lives. so on and so forth
-   if you call `Bundle.main`, that will return the "product" or the bundle containing the current executable. you generally don't want to call this anymore unless you know you want the app layer bundle


## Fetching latest


You have a dependency pointed to specific branch and you push some commits on the dependency's branch. But Xcode and SPM would always use the `cache` version of that dependency. Since we didn't go for `SemVer` approach and just a branch SPM and xcode isn't smart enough to automatically pull in latest or fetch origin. Unless you nuke the cache and SPM manifest metadata with git commits for every package dependency located in `~/Library` directory.

You can avoid that hassle by just updating your packages and invalidating previous cache and Xcode / SPM is smart enough to abide by those SemVer rules or just update to the latest commit on the specified branch. 
Note: Manually selecting the library and right clicking to select option `Update` doesn't update it for me Xcode 15 beta 6 with package dependency defined using a `branch: "branch_name"`

You can do update by following this option in the menu bar.
```
Xcode ->  File -> 
Packages ->
Update to Latest Package versions
```


## Errors

### Module Cache Path 
When you changed the whole package name & folder. Xcode clean build doesn't work sometimes when you run `swift run package_name` on Command Line.
So delete the `.build` directory.
[PCH was compiled with module cache path error](https://stackoverflow.com/questions/57080473/pch-was-compiled-with-module-cache-path-error)


### Packages Not downloaded

```log
Not able to download packages properly.
```

Option in Menu bar.
Xcode ->  File -> Packages -> 
`Reset package caches`
& even not working then select `resolve packages`

### Artifact not mapped with Binary Target

```log
Binary target 'LibraryName' could not be mapped to an artifact with the expected name 'LibraryName'
```

Deleting `~/Library/org.swift.swiftpm` helped for us
```sh
rm -rf ~/Library/org.swift.swiftpm
```

https://developer.apple.com/forums/thread/711597


```log
**security-spm-client-manifest**

Revision 37351b7ac065f11cd70c41ca7610539a82856ddf for security-spm-client-manifest remoteSourceControl https://github.company.com/contentsecurity/security-spm-client-manifest.git version 7.3.5 does not match previously recorded value 00a34dfabec0d11baebsafasfce96793e984a8b

Fetching from https://github.company.com/contentsecurity/security-spm-client-manifest.git (cached)
```



### missing required module ''

```bash
<unknown>:0: error: missing required module 'HLSObjectiveC'
```

*This* usually happens if the target / library sources have an import product_name / library and you haven't defined its dependency in the `target` package.swift

```swift
// Logging.swift
import productName


// Package.swift

.target(
	name: "Logging",
	dependencies: [.product(name: "productName",
							package: "packageName")],
	path: "Sources/Logging"
)
```

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

```swift]
import DummyUnit
```
For more information on Frameworks refer my other [docs](ios/library/framework.md)





## Local Package dependency

You can point a swift package to local option in order to do faster prototyping instead of waiting for xcode to close / fetch / resolve SPM package directory and then make it usable to edit a file. 

+1 Less `.xcodeproj` `xcworkspace` headaches.


## Pitfalls


[Some pitfalls of using SPM and Build Configuration in Xcode](https://www.sobyte.net/post/2022-10/spm-in-xcode/)

## Resources


[Basics](https://medium.com/server-side-swift-and-more/swift-package-manager-basics-c653de716e13)


https://www.youtube.com/watch?v=QmBZ9wJguS4

Caching and Purge caching
https://blog.eidinger.info/swift-package-purge-cache

[SwiftPM: Same sources, multiple targets](https://forums.swift.org/t/swiftpm-same-sources-multiple-targets/48810)
