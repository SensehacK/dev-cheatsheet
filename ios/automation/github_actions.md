# GitHub Actions

## Workflow Example

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



## Runners

Checking what runners are available for Github Actions
https://github.com/actions/runner-images

## Workflow

### Manual trigger

Running a workflow to run manually
[Github docs](https://docs.github.com/en/actions/using-workflows/manually-running-a-workflow)

### Filtering

Branch specific wildcards

```yaml
on:
  pull_request:
    # Sequence of patterns matched against refs/heads
    branches:    
      - main
      - develop
      - 'releases/**'
```


[github actions doc](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#example-including-branches)


## Github Context

You can get the current github context by referring this [doc on github website](https://docs.github.com/en/actions/learn-github-actions/contexts)

## Specify Xcode Version

You can use this action before running your command
https://github.com/marketplace/actions/setup-xcode-version

```log
package 'swift-docc' is using Swift tools version 5.9.0 but the installed version is 5.8.0
```

Sometimes its more important to be on specific xcode version or swift package tools
