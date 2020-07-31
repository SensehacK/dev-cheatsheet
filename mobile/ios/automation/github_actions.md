# GitHub Actions

Github Actions

This is the script I’m using for building on Github Actions workflow.

```yaml
name: Swift

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

defaults:
  run:
    shell: bash
    working-directory: ./src/iOS/HealthSense

jobs:
  build:
    runs-on: macos-latest

    steps:
    - uses: actions/checkout@v2

    - name: Shell Info
      run: cd $PWD && ls

    - name: Dependency installation
      run: pod install

    - name: Xcode list project structure
      run: xcodebuild -list -project  HealthSense.xcodeproj

    - name: Xcode Actual Build
      run: xcodebuild clean build test -workspace HealthSense.xcworkspace -scheme HealthSenseCI -destination "platform=iOS Simulator,OS=13.3,name=iPhone 11" ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO -skip-testing:HealthSenseUITests

    - name: Displays cocoapods version
      run: pod --version
```

