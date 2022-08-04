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

swift test --filter TrackViaNetworkUnitTests

```
swift test --filter TrackViaNetworkUnitTests -sdk /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS15.2.sdk  -target arm64-apple-ios15.2
```

swift test --filter TrackViaNetworkUnitTests -target arm64-apple-ios15.2


Running this command for tests.

```
xcodebuild -scheme TrackViaNetworkTestKit test -sdk iphonesimulator -destination 'platform=iOS Simulator,name=iPhone 13'
```


Running specific package tests 

```
xcodebuild test -scheme TrackViaNetwork-Package -sdk iphonesimulator15.2 -destination "OS=15.2,name=iPhone 13" -only-testing:"TrackViaNetworkIntegrationTests"

```

Running specific class unit tests 

```
xcodebuild test -scheme TrackViaNetwork-Package -sdk iphonesimulator15.4 -destination "OS=15.4,name=iPhone 13" -only-testing:"TrackViaNetworkIntegrationTests/AuthenticationServiceIntegrationTests/testLogin" -quiet
```


No verbose option with xcode build command
> xcodebuild -quiet

Or use pipeline with external tool called `xcpretty`
> | xcpretty

[Swift package Tests](https://www.jessesquires.com/blog/2021/11/03/swift-package-ios-tests/)

## Arguments 


[CLI arguments](https://rderik.com/blog/command-line-argument-parsing-using-swift-package-manager-s/)

## Environment Variables

Setting environment variables on the project and reading from them via Xcode.

Setting variables
```export TEST_RUNNER_QAENV=EnvironmentQA1```

[xcode build Env variables](https://stackoverflow.com/questions/40722756/passing-arguments-to-ios-tests-with-xcodebuild)

## Resources

[10-tips-to-run-swift-CLI](https://betterprogramming.pub/10-tips-to-run-swift-from-your-terminal-b5832cd9cd8c)


[Swift Executables](https://www.fivestars.blog/articles/ultimate-guide-swift-executables/)


[cli-xcodeBuild](https://tarikdahic.com/posts/build-ios-apps-from-the-command-line-using-xcodebuild/)

[xcodebuild arguments](https://www.macstadium.com/blog/making-sense-of-xcodebuild-arguments)


## Errors

building on mac OS version.

```
error: the library 'TrackViaCore' requires macos 10.10, but depends on the product 'CryptoSwift' which requires macos 10.12; consider changing the library 'TrackViaCore' to require macos 10.12 or later, or the product 'CryptoSwift' to require macos 10.10 or earlier.
error: the library 'TrackViaNetwork' requires macos 10.10, but depends on the product 'Moya' which requires macos 10.12; consider changing the library 'TrackViaNetwork' to require macos 10.12 or later, or the product 'Moya' to require macos 10.10 or earlier.
error: the library 'TrackViaNetwork' requires macos 10.10, but depends on the product 'Alamofire' which requires macos 10.12; consider changing the library 'TrackViaNetwork' to require macos 10.12 or later, or the product 'Alamofire' to require macos 10.10 or earlier.
error: fatalError
```


-sdk /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS15.2.sdk  -target arm64-apple-ios15.2


Schemes available for running

Information about workspace "TrackVia-iOS-Network":
    Schemes:
        TrackViaNetwork
        TrackViaNetwork-Package
        TrackViaNetworkTestKit
        
        

```
xcodebuild: error: Scheme TrackViaNetworkTestKit is not currently configured for the test action.
```


### xcrun: error: unable to find utility "xctest", not a developer tool or in PATH
Making sure we set our command line tools appropriately in Xcode when running from Terminal or having two different Xcode.

[xcrun: error](https://stackoverflow.com/questions/61501298/xcrun-error-unable-to-find-utility-xctest-not-a-developer-tool-or-in-path)