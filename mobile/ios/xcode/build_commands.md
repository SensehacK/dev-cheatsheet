# Build Commands

## Main Command

`xcodebuild clean build test -workspace iOSTravisCI.xcworkspace -scheme iOSTravisCI -sdk iphonesimulator -destination "platform=iOS Simulator,OS=12.1,name=iPhone 7" ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO`

## Build Command

`xcodebuild -scheme iOSTravisCI -workspace iOSTravisCI.xcworkspace/ build`

## Build for test Command

`xcodebuild build-for-testing -workspace iOSTravisCI.xcworkspace -scheme iOSTravisCI -destination generic/platform=iOS`

## Test Command

`xcodebuild -scheme iOSTravisCI -workspace iOSTravisCI.xcworkspace/ test`

## Health Sense Project

```yaml
xcodebuild -scheme HealthSense -workspace HealthSense.xcworkspace/ -allowProvisioningUpdates build

xcodebuild -scheme HealthSense -workspace HealthSense.xcworkspace/ build




Working Xcode Build locally
xcodebuild clean build test -workspace HealthSense.xcworkspace -scheme HealthSenseCI -destination "platform=iOS Simulator,OS=13.3,name=iPhone 11" ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO


xcodebuild clean build test -workspace HealthSense.xcworkspace -scheme HealthSenseCI -sdk universal -destination "platform=iOS Simulator,OS=13.3,name=iPhone 11" ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO



xcodebuild clean build test -workspace HealthSense.xcworkspace -scheme HealthSenseCI -destination "platform=iOS Simulator,OS=13.3,name=iPhone 11" ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO -skip-testing:HealthSenseUITests
```

