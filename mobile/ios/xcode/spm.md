# spm


## Setup

You can utilized the Xcode SPM functionality in built with version 11

Great for linking different packages and frameworks to Xcode with first class support.

No messy .xcodeproj / .xcworkspace file

Create 



## Directory

Cache directory for SPM

> ~/Library/Caches/org.swift.swiftpm/.

[Install size](https://forums.swift.org/t/shrinking-toolchain-install-size/44771)


## Errors


When you changed the whole package name & folder. Xcode clean build doesn't work sometimes when you run `swift run package_name` on Command Line.
So delete the `.build` directory.
[PCH was compiled with module cache path error](https://stackoverflow.com/questions/57080473/pch-was-compiled-with-module-cache-path-error)


## Resources


[Basics](https://medium.com/server-side-swift-and-more/swift-package-manager-basics-c653de716e13)

