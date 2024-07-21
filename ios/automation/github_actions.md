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

Checking what runners images are available for [Github Actions](https://github.com/actions/runner-images)


## Workflow

### Manual trigger

Running a workflow to run manually
[Github docs](https://docs.github.com/en/actions/using-workflows/manually-running-a-workflow)

```yaml
on: workflow_dispatch
```

> Note: This event will only trigger a workflow run if the workflow file is on the default branch.

### Reasoning 

Reasoning behind why something like this is needed. As I had to explain my reasoning with my team.

> alright not trying to be difficult, just trying to understand what work flows you need to run before you open a pull request?

Answer

Nw let me explain my train of thoughtScenario 1:  

- We start testing some work on GA workflow, but in order to test it we have to open a PR.
- Once that's open we would push commits with new changes to see how it reacts & wait for the builder queue to run it successfully.
- Which sends out a slack workflow notification (polluting the channel) ( we can filter out notifications only if the PR is up or has a specific tag )
- By having an option of manual trigger -> a person can work on a dirty branch do 4 - 7 commits and actually open a PR with 1 commit change (we can do rebase or squash) too but that's a total diff strategy.

Scenario 2:  

- We have manual workflows with `Input` like enabled_logging, `deploy_docs` or `send_slack_notification`  or `update_slack_channel_description_tag` or `tag / release` manually
- We can have all this workflows with a conditional if or provide a manual trigger with input so that it runs a specific workflow and not run all `n` number of workflows which aren't necessary.
- eg. when 2 tasks are dependent on 1 task we can do conditional `depends` but if a `deploy docc`  job isn't dependent on tests or other builds we can run it independently without having the whole workflow job failed.
- This saves us compute time, checking back on GA for jobs to be completed or queued up and less slack notifications.
- Essentially we won't have to wait for 5 mins in order to `build, test, deploy docs` just to update the `tag` job on slack. We can essentially leap frog our way to directly run independent jobs with more finer control with `manual trigger` instead of Be_All_Generalized_Rule (like: if main has new commits run these 2 workflows)

All these scenarios could be supported with `manual_triggers` and that's the stepping stone for future enhancements on GA automation.


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
[GA | workflow check xcode version](https://github.com/marketplace/actions/setup-xcode-version)

```log
package 'swift-docc' is using Swift tools version 5.9.0 but the installed version is 5.8.0
```

Sometimes its more important to be on specific xcode version or swift package tools

## Errors

### Resource not accessible by integration

```log
"Resource not accessible by integration" on github post /repos/{owner}/{repo}/actions/runners/registration-token API]
```

Was solved by providing the write permission in YAML file

```yaml
name: "test-action"
on: 
  pull_request:
jobs:
    lint:
        runs-on: macOS-builder
        permissions:
          contents: read
          pull-requests: write
          repository-projects: read
```

[SO](https://stackoverflow.com/questions/70435286/resource-not-accessible-by-integration-on-github-post-repos-owner-repo-ac)