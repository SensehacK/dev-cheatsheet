# Fastlane


## Setup

Ruby bundler installation is a prerequisite. To install and run fastlane commands on macOS or any unix environment.

## Commands


```sh
bundle exec fastlane ea

bundle exec fastlane increment_build

bundle exec fastlane increment_version
```



## Setup

[fastlane docs](https://docs.fastlane.tools/#)
[github actions integration](https://docs.fastlane.tools/best-practices/continuous-integration/github/)

## Issues



## Environment Variables

Make `dotEnv` `.env` file in order to quickly import appropriate `Environment` variables in the build system.

Fastfile config file
```ruby

platform :ios do
  before_all do
    Dotenv.load ".env.ios"
  end

  lane: beta do
    match
    deliver
  end
end
```

https://docs.fastlane.tools/best-practices/keys/

https://www.runway.team/blog/better-fastlane-with-environments



## Resources

[Implementing fastlane from nothing to App Store](https://www.youtube.com/watch?v=6Jz-Ywxki0U)

[Raywenderlich](https://www.raywenderlich.com/1259223-fastlane-for-ios)

[Docs](https://docs.fastlane.tools/actions/pilot/#pilot)

[Medium](https://medium.com/@vizllx/build-test-deliver-a-complete-guideline-for-ios-ci-cd-5fa02bffa7ce)

[Another Medium article for Github Actions and fastlane](https://litoarias.medium.com/continuous-delivery-for-ios-using-fastlane-and-github-actions-edf62ee68ecc)

[Runway - How to set up a CI/CD pipeline for your iOS app using fastlane and GitHub Actions](https://www.runway.team/blog/how-to-build-the-perfect-fastlane-pipeline-for-ios)


[Gitlab and Fastlane](https://about.gitlab.com/blog/2019/03/06/ios-publishing-with-gitlab-and-fastlane/)

[A Complete Guide to iOS App Auto Deployment with CI-CD](https://blog.canopas.com/a-complete-guide-to-ios-app-auto-deployment-with-ci-cd-b5dc516ba41d)