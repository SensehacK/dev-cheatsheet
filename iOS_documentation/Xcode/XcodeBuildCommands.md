# Xcode Build Commands

## Main Command

```xcodebuild clean build test -workspace iOSTravisCI.xcworkspace -scheme iOSTravisCI -sdk iphonesimulator -destination "platform=iOS Simulator,OS=12.1,name=iPhone 7" ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO```

## Build Command

```xcodebuild -scheme iOSTravisCI -workspace iOSTravisCI.xcworkspace/ build```

## Build for test Command

```xcodebuild build-for-testing -workspace iOSTravisCI.xcworkspace -scheme iOSTravisCI -destination generic/platform=iOS```

## Test Command

```xcodebuild -scheme iOSTravisCI -workspace iOSTravisCI.xcworkspace/ test```