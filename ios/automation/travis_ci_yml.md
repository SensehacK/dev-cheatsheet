# Travis CI

This is the script I’m using for building on Xcode Travis CI workflow. You could also refer to my older doc regarding TravisCI Timeline. [TravisCITimeline.md](traviscitimeline.md)

## Normal

```yaml
os: osx
osx_image: xcode11.3
language: swift

before_install: gem install cocoapods

podfile: src/iOS/HealthSense/Podfile
xcode_workspace: src/iOS/HealthSense/
xcode_scheme: HealthSenseCI
xcode_destination: platform=iOS Simulator,OS=13.3,name=iPhone 11


# Build the main app, which happens to depend on the test cases.
script: xcodebuild clean build test -workspace src/iOS/HealthSense/HealthSense.xcworkspace -scheme HealthSenseCI -destination "platform=iOS Simulator,OS=13.3,name=iPhone 11" ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO -skip-testing:HealthSenseUITests


after_success:
  - bash <(curl -s https://codecov.io/bash)
```

## Pods Directory

Rough Work

```text
os: osx
osx_image: xcode11.3
language: swift

before_install: gem install cocoapods

install:
- pwd
- cd src/iOS/HealthSense
- pod install

podfile: Podfile
xcode_scheme: HealthSenseCI
xcode_destination: platform=iOS Simulator,OS=13.3,name=iPhone 11


# Build the main app, which happens to depend on the test cases.
script: xcodebuild clean build test -workspace HealthSense.xcworkspace -scheme HealthSenseCI -destination "platform=iOS Simulator,OS=13.3,name=iPhone 11" ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO -skip-testing:HealthSenseUITests
```

