# Danger

## Intro

[github | danger](https://github.com/danger/swift)

[using-swiftlint-and-danger-for-swift-best-practices](https://candost.blog/using-swiftlint-and-danger-for-swift-best-practices/)


## iOS

iOS Getting started

[danger docs | iOS App](https://danger.systems/swift/tutorials/ios_app.html)

[danger docs | getting_started](https://danger.systems/guides/getting_started.html)

## Gitlab

[gitlab | dangerbot](https://docs.gitlab.com/ee/development/dangerbot.html)


Gitlab integration
[gitlab |  danger bot](https://danger.systems/swift/usage/gitlab.html)

[getting_started - creating-a-dangerfile](https://danger.systems/swift/guides/getting_started.html#creating-a-dangerfile)



### CI

[medium | your-guide-to-danger-swift-on-ci](https://medium.com/kinandcartacreated/your-guide-to-danger-swift-on-ci-83e3f5136a9a#a5f1)

## Config


[Sample Danger file](https://gist.github.com/candostdagdeviren/e49271e6a4b80f93f3193af89d10f4b1)


[danger-in-ci-automate-your-mobile-code-reviews](https://blog.appcircle.io/article/danger-in-ci-automate-your-mobile-code-reviews)


[Best Practices for Swiftlint and Danger](https://candost.blog/using-swiftlint-and-danger-for-swift-best-practices/) 


## Implementation

[how-to-implement-danger-in-swift](https://betterprogramming.pub/how-to-implement-danger-in-swift-fb8ea070ceb6)

[how-to-implement-danger-in-swift](https://cctplus.dev/how-to-implement-danger-in-swift/)

[medium | your-guide-to-danger-swift-on-ci](https://medium.com/kinandcartacreated/your-guide-to-danger-swift-on-ci-83e3f5136a9a)



Danger plugins
[avanderlee | danger-plugins](https://www.avanderlee.com/optimization/danger-plugins/)



## local setup


x86 vs ARM issues with Danger / xcode / terminal / homebrew

To install the package.

```sh
brew install danger/tap/danger-swift
```


Make sure you have homebrew installed in x86 mode rather than ARM mode. You can check by running [this command](../../tools/terminal/shell#Arch)


This command to run danger swift with base branch as `main`. My setup requires `swift-lint` installed globally or locally or else danger won't parse `swift-lint` command.
It's complicated given how our project workspace, SPM, frameworks are organized in our project.


```sh
danger-swift local -b main
```

A big architecture decision would be needed to be made whether we want to decouple our plugin - checks or just have it build locally before every project gets compiled or with PR.



## Commands


Edit a workspace

```sh
danger-swift edit
```

Make a local comparison

```sh 
danger-swift local -b main
```


