# Framework Errors

## Intro

## Framework Arch Mismatch

`Could not find module for target 'x86_64-apple-ios-simulator'`

[Could not find module for target 'x86_64-apple-ios-simulator'](https://stackoverflow.com/questions/56957632/could-not-find-module-for-target-x86-64-apple-ios-simulator)

Probably best to ask the vendor to support the appropriate SDK option

```log
Could not find module '' for target 'arm64-apple-ios-simulator'; found: x86_64-apple-ios-simulator, at: /Users/username/Library/Developer/Xcode/DerivedData/ProjectPlatform-ephpdgxzgtsjofhisorxmacihwzc/Index.noindex/Build/Products/Debug-iphonesimulator/OHHTTPStubs.framework/Modules/OHHTTPStubs.swiftmodule
```

## Cannot load module build with SDK Version mismatch

```log
**Showing All Messages**

/Users/username/git/github_internal/Projectplatform_ios/ProjectPlatformTests/ConfigEndpointsTest.swift:14:8: Cannot load module 'OHHTTPStubs' built with SDK 'iphonesimulator16.4' when using SDK 'iphonesimulator17.0': /Users/username/Library/Developer/Xcode/DerivedData/ProjectPlatform-ephpdgxzgtsjofhisorxmacihwzc/Build/Products/Debug-iphonesimulator/OHHTTPStubs.framework/Modules/OHHTTPStubs.swiftmodule/x86_64-apple-ios-simulator.swiftmodule
```

## Missing package product

Local Swift Packages Error for each package dependency Missing package product
https://stackoverflow.com/questions/69281786/local-swift-packages-stopped-working-in-xcode-13/69793517#69793517

## Library not loaded dyld cache

dyld: Library not loaded

```log
dyld[14624]: Library not loaded: @rpath/PromiseKit.framework/PromiseKit
  Referenced from: <-B900-2B6DBEB96FE0> /private/var/containers/Bundle/Application/-A0C7-E660638AF789/TestUI.app/Frameworks/SClient.framework/SClient
  Reason: tried: '/usr/lib/swift/PromiseKit.framework/PromiseKit' (no such file, not in dyld cache), 
```

Even if you did delete the rogue references and readded it again. You need to make sure you delete your derived data on your xcode and somehow uninstall your app on your test device.

SPM `update to latest versions` definitely helps if there's a version change and then the previous cache gets invalidated. But its a hit or miss sometimes.
Important thing is to find the right cache path and delete the cache in order to get a proper reference of the dynamic library linking on runtime. Or else you'll get a crash.

[sarunw | how-to-fix-dyld-library-not-loaded-error](https://sarunw.com/posts/how-to-fix-dyld-library-not-loaded-error/)

## Library duplicate Choosing one

So somethings there are two frameworks being added in Xcode dynamic library but it leads to linking error. 
We are having this issue because SPM internal dependencies dependency hasn't exposed it appropriately as a framework. So hence the frameworks are being added twice since the framework team didn't expose the PromiseKit properly so we had to explicitly add the `framework` in order to get the right xcframework.

```log
objc[17097]: Class _ is implemented in both TestUI.app/Frameworks/other.framework/) and TestUI.app/TestUI (0x1026b3620). One of the two will be used. Which one is undefined.
```

[Copied from SO | Post](https://stackoverflow.com/a/71755828/5177704)

For me non of the above solutions worked because I use Carthage dependency manager.

This fixed the issue for me:

1. under general tab of the project settings, make MyFramework.framework -> do not embed
2. in linked binaries under build phases tab of your project setting, find same framework and instead of 'required' make it 'optional'

The framework is once embedded in the project by one dynamic dependency and once by an static dependency. And it ends up being integrated in the bundle twice. You should be able to pin point which framework you need to make optional and the error shall disappear.

For example if you are using both app center crashes and data dog crashes (just an example) in your project, you will end up both those dependencies requiring 'PLCrashReporter.framework'. this is used by 'DataDogCrashReporter' that is a dynamic library and AppCenterCrashReporter that is a static library. I made 'DataDogCrashReporter' an optional and didn't embed it any more.


## CFBundleIdentifier Collision

```text
"CFBundleIdentifier Collision. There is more than one bundle with the CFBundleIdentifier value com.companyname.projectName under the application ProjectName.app"
```

### Cause

It happens if your HostApp embeds a framework which has been also embedded in some of the frameworks which are also being embedded in HostApp. For example,

1. Host `H` embeds framework `F1` and framework `F2`
2. Framework `F1` embeds framework `F2`
3. Thus, Framework `F2` will be duplicated in bundle after IPA generated

### Solution

Only HostApp but no other frameworks should embed any dependent frameworks in their respective Build Phase. So,

1. Go to Build Phase tab for `F1`
2. Remove `F2` from `Embed Frameworks` step, or remove full step
3. Go to General tab for `F1`
4. Select Frameworks, Libraries and Embedded Content
5. Select `Do Not Embed` option for `F2`

Have a clean build.
[SO | Post Answer copied](https://stackoverflow.com/a/61623753/5177704)



## Compiled module was created by a different version of the compiler


```log
Compiled module was created by a different version of the compiler '5.9.0.128.108'; rebuild 'PlayerPlatform' and try again: /Users/ksave957/Library/Developer/Xcode/DerivedData/X2-asssnibtvfhvubfewbpdxmzglydp/Index.noindex/Build/Products/Debug-iphoneos/PlayerPlatform.framework/Modules/PlayerPlatform.swiftmodule/arm64-apple-ios.swiftmodule


// Another 

  
/Users/ksave957/git/cloud/XTV/X2/X2/PlayerPlatformPlayer.swift:15:8: Cannot load module 'PlayerPlatform' built with SDK 'iphoneos17.0' when using SDK 'iphoneos17.4': /Users/ksave957/Library/Developer/Xcode/DerivedData/X2-asssnibtvfhvubfewbpdxmzglydp/Build/Products/Dev-iphoneos/PlayerPlatform.framework/Modules/PlayerPlatform.swiftmodule/arm64-apple-ios.swiftmodule
```