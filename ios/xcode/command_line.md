Command Line



## Usage



Default documentation
> xcode-build -help

> man xcode-build


### Build

Cleaning the project.

> xcodebuild clean

Listing all schemes
xcodebuild -list

### Tests

To run all tests
> swift test


To run specific tests
> swift test --filter testTargetName

swift test --filter product_nameNetworkUnitTests

```bash
swift test --filter product_nameNetworkUnitTests -sdk /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS15.2.sdk  -target arm64-apple-ios15.2
```

swift test --filter product_nameNetworkUnitTests -target arm64-apple-ios15.2


Running this command for tests.

```bash
xcodebuild -scheme product_nameNetworkTestKit test -sdk iphonesimulator -destination 'platform=iOS Simulator,name=iPhone 13'
```


Running specific package tests 

```bash
xcodebuild test -scheme product_nameNetwork-Package -sdk iphonesimulator15.2 -destination "OS=15.2,name=iPhone 13" -only-testing:"product_nameNetworkIntegrationTests"

```

Running specific class unit tests 

```bash
xcodebuild test -scheme product_name-Package -sdk iphonesimulator15.4 -destination "OS=15.4,name=iPhone 13" -only-testing:"product_nameNetworkIntegrationTests/AuthenticationServiceIntegrationTests/testLogin" -quiet
```


Embedded into SPM project dependencies in `.xcworkspace`. Spent around 45 mins + just to figure out why it was erroring out and I think so I had 10+ different variants of Xcode Build Test CLI commands before landing what I was doing wrong. 
I missed providing `-workspace` argument, xcode couldn't decipher directly based off the `-scheme`  since the project I work on is a poly repo - which has cyclical dependency of 8 layers including the main - iOS lifecycle layer. So it was necessary to provide more context to the Xcode - cli. 
```bash
xcodebuild test -workspace product_name-iOS.xcworkspace -scheme product_scheme -sdk iphonesimulator16.2 -destination "OS=16.2,name=iPhone 14" -only-testing:"product_nameViewModelTests/EnvironmentListViewModelTests/test_environmentVariableDefinedToSkipFlakyTests"
```

No verbose option with xcode build command
> xcodebuild -quiet

Or use pipeline with external tool called `xcpretty`
> | xcpretty

[Swift package Tests](https://www.jessesquires.com/blog/2021/11/03/swift-package-ios-tests/)

## Arguments 


[CLI arguments](https://rderik.com/blog/command-line-argument-parsing-using-swift-package-manager-s/)

[environment_Variables](environment_Variables.md)

## Resources

[10-tips-to-run-swift-CLI](https://betterprogramming.pub/10-tips-to-run-swift-from-your-terminal-b5832cd9cd8c)


[Swift Executables](https://www.fivestars.blog/articles/ultimate-guide-swift-executables/)


[cli-xcodeBuild](https://tarikdahic.com/posts/build-ios-apps-from-the-command-line-using-xcodebuild/)

[xcodebuild arguments](https://www.macstadium.com/blog/making-sense-of-xcodebuild-arguments)


## Errors

building on mac OS version.

```
error: the library 'product_nameCore' requires macos 10.10, but depends on the product 'CryptoSwift' which requires macos 10.12; consider changing the library 'product_nameCore' to require macos 10.12 or later, or the product 'CryptoSwift' to require macos 10.10 or earlier.
error: the library 'product_nameNetwork' requires macos 10.10, but depends on the product 'Moya' which requires macos 10.12; consider changing the library 'product_nameNetwork' to require macos 10.12 or later, or the product 'Moya' to require macos 10.10 or earlier.
error: the library 'product_nameNetwork' requires macos 10.10, but depends on the product 'Alamofire' which requires macos 10.12; consider changing the library 'product_nameNetwork' to require macos 10.12 or later, or the product 'Alamofire' to require macos 10.10 or earlier.
error: fatalError
```


-sdk /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS15.2.sdk  -target arm64-apple-ios15.2


Schemes available for running

Information about workspace "product_name-iOS-Network":
    Schemes:
        product_nameNetwork
        product_nameNetwork-Package
        product_nameNetworkTestKit
        
        

```
xcodebuild: error: Scheme product_nameNetworkTestKit is not currently configured for the test action.
```


### xcrun: error: unable to find utility "xctest", not a developer tool or in PATH
Making sure we set our command line tools appropriately in Xcode when running from Terminal or having two different Xcode.

[xcrun: error](https://stackoverflow.com/questions/61501298/xcrun-error-unable-to-find-utility-xctest-not-a-developer-tool-or-in-path)