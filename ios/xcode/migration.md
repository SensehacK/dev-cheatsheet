#  Migration
## SDK

### iOS 16

https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/ios_16/

## Migration

### Swift 5

https://www.swift.org/migration-guide-swift5/

https://www.avanderlee.com/swift/updating-swift-5/

https://medium.com/thecreateschool/migrating-from-swift-4-to-swift-5-2f425b99436b


### Swift 2 - 3

https://www.swift.org/migration-guide-swift3/

https://medium.com/@DoorDash/tips-and-tricks-for-migrating-from-swift-2-to-swift-3-c67a8520dbac

https://navyuginfo.com/upgrade-ios-10-now-pre-requisites-steps/



### VisionOS

[Migrating my SwiftUI App to VisionOS in 2 Hours](https://www.fline.dev/migrating-my-swiftui-app-to-visionos/)

## Xcode 16


### AVFoundation

Had to provide stub conformance to 

```swift
extension AVContentKeyRequest: ContentKeyRequestRepresentable {

    /// Default key identifier somehow calms the swift compiler in Xcode 16
    @objc
    var identifier: Any? {
        "zephyr.drm.key"
    }
```

>  we'll table this until we comb through everything with Xcode 16

Saw this way too late and was in the weeds why xcode is behaving like that. tried swift clang version and everything but no avail.
It's just Xcode 16 uses new clang version & Swift 6.0 by default but it shouldn't matter since `internal_spm` package is using 5.8

It seems the issue arises due to clang mismatch with xcode throwing a compile time error.

Surprisingly Xcode 15 or 16 doesn't complain about this error on `internal_xcodeproj` with  `internal_spm`  pointed to this branch.  
maybe because `internal_xcodeproj` is a proper `Xcode Proj` and takes the clang / llvm settings from the build settings. Sadly with a independent swift package like internal_spm we can control that variable or have explicit build settings to control what Xcode builds the `executable` at the runtime with the package.

Maybe we can squeeze in an `.xconfig` file which overrides it but I have exhausted my google foo for the day 👎 

Better option is just to adopt Xcode 16 and update the `// swift-tools-version: 5.8` to `6.0` and work on that migration than this PITA apple does with `beta` versions. Or maybe they'll fix it somehow in the gold master release.

#### Update
I was able to solve this via `compiler` [wildcard check](ios/library/wildcard_checks#check%20compiler) 

Apparently I was able to solve this via wildcard check / compiler directive.
But swift, iOS, xcode those things don't work. For me the `#compiler` worked.

```swift
#if compiler(>=6.0)
```

Too much testing for [mamba 1.5.9](https://github.com/Comcast/mamba/releases/tag/1.5.9) update for tvOS 18/ xcode 16. That lead to this rabbit hole of apple documentation change and downloading Xcode 16 beta 3, iOS 18, tvOS18 beta simulators and juggling through both xcodes to get it building. While battling SPM cache issues. Sometimes I hate apple development.

But at least now it should compile properly with warnings on Xcode 15 & 16.
