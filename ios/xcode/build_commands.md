# Build Commands

## *Main* Command

```sh
# Xcode 12
xcodebuild clean build test -workspace iOSTravisCI.xcworkspace -scheme iOSTravisCI -sdk iphonesimulator -destination "platform=iOS Simulator,OS=12.1,name=iPhone 7" 

ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO

# Xcode 15.3
xcodebuild -scheme "PCore" -destination "platform=iOS Simulator,OS=17.4,name=iPhone 15" build
```


## Build Command

```bash
xcodebuild -scheme iOSTravisCI -workspace iOSTravisCI.xcworkspace/ build
```

## Build for test Command

```bash
xcodebuild build-for-testing -workspace iOSTravisCI.xcworkspace -scheme iOSTravisCI -destination generic/platform=iOS
```



## Test Command

```bash
xcodebuild -scheme iOSTravisCI -workspace iOSTravisCI.xcworkspace/ test
```


## Health Sense Project

```yaml
xcodebuild -scheme HealthSense -workspace HealthSense.xcworkspace/ -allowProvisioningUpdates build

xcodebuild -scheme HealthSense -workspace HealthSense.xcworkspace/ build
```


#### Working Xcode Build locally

```bash
xcodebuild clean build test -workspace HealthSense.xcworkspace -scheme HealthSenseCI -destination "platform=iOS Simulator,OS=13.3,name=iPhone 11" ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO


xcodebuild clean build test -workspace HealthSense.xcworkspace -scheme HealthSenseCI -sdk universal -destination "platform=iOS Simulator,OS=13.3,name=iPhone 11" ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO


xcodebuild clean build test -workspace HealthSense.xcworkspace -scheme HealthSenseCI -destination "platform=iOS Simulator,OS=13.3,name=iPhone 11" ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO -skip-testing:HealthSenseUITests
```


## Resources


[xcode terminal commands](xcode.md)

[xcodebuild destination cheatsheet](https://mokacoding.com/blog/xcodebuild-destination-options/)