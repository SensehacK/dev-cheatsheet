# Swift Package Manager

## Intro

Versatile yet out of beta package manager. Great support in built in Xcode IDE. 
Still initial adoption pain back in 2020, 2021. I think so past two years it has matured quite a bit.





## Setup

You can utilized the Xcode SPM functionality in built with version 11

Great for linking different packages and frameworks to Xcode with first class support.

No messy .xcodeproj / .xcworkspace file

Create 



## Directory

Cache directory for SPM

> ~/Library/Caches/org.swift.swiftpm/.

[Install size](https://forums.swift.org/t/shrinking-toolchain-install-size/44771)

## Bundling

A note with Swift package manager bundling directories.

Swift Package Manager world, bundling basically boils down to the following:

-   `Bundle.module` returns the bundle relative to the call site. so if you call that in `FrameworkCore/AppInfo.swift` it will return the `FrameworkCore` bundle since that file and type are associated with that bundle. if you call it in `FrameworkCoreTestKit/Mock.swift` it will return the test kit bundle since that's where that file lives. so on and so forth
-   if you call `Bundle.main`, that will return the "product" or the bundle containing the current executable. you generally don't want to call this anymore unless you know you want the app layer bundle


## Errors

### Module Cache Path 
When you changed the whole package name & folder. Xcode clean build doesn't work sometimes when you run `swift run package_name` on Command Line.
So delete the `.build` directory.
[PCH was compiled with module cache path error](https://stackoverflow.com/questions/57080473/pch-was-compiled-with-module-cache-path-error)


### Packages Not downloaded
```
Not able to download packages properly.
```
Option in Menu bar.
Xcode ->  File -> Packages -> 
`Reset package cache`
& even not working then select `resolve packages`

### Artifact not mapped with Binary Target

```
Binary target 'LibraryName' could not be mapped to an artifact with the expected name 'LibraryName'
```

Deleting `~/Library/org.swift.swiftpm` helped for us
```sh
rm -rf ~/Library/org.swift.swiftpm
```

https://developer.apple.com/forums/thread/711597


## Resources


[Basics](https://medium.com/server-side-swift-and-more/swift-package-manager-basics-c653de716e13)


https://www.youtube.com/watch?v=QmBZ9wJguS4