# Gitlab CI Yaml


We can specify our CI instructions for Gitlab CI to process those files and execute that structure accordingly.


## Initialize
Create `gitlab-ci.yml` file in your root directory of your repository.

[YAML doc](https://docs.gitlab.com/ee/ci/yaml/)
[YAML CI/CD](https://docs.gitlab.com/ee/development/cicd/cicd_reference_documentation_guide.html#yaml-reference-structure)

## Execute Locally


Dependencies needed to be run in order to run locally.

> brew install gitlab-runner

This will install the necessary components for setting up local workspace in order to parse the job locally which is defined in `.yml` file.

[Shell](https://docs.gitlab.com/runner/executors/shell.html)

[gitlab Ci local](https://bagong.gitlab.io/posts/run-gitlab-ci-locally/)

[Gitlab CI test local](https://www.lambdatest.com/blog/use-gitlab-ci-to-run-test-locally/)

[Test Local Medium](https://medium.com/@umutuluer/how-to-test-gitlab-ci-locally-f9e6cef4f054)

[Basic gitlab CI config iOS](https://blogs.perficient.com/2017/05/24/basic-gitlab-ci-configuration-for-ios-projects/)

[gitlab blog publish fastlane CI](https://about.gitlab.com/blog/2019/03/06/ios-publishing-with-gitlab-and-fastlane/)

[youtube gitlab CI dev to prod](https://www.youtube.com/watch?v=gr76MNXZJfQ)


## Documentation

[gitlab docs environment variables](https://docs.gitlab.com/ee/administration/environment_variables.html#environment-variables)

[gitlab docs variables](https://docs.gitlab.com/ee/ci/variables/index.html)

[gitlab environment](https://docs.gitlab.com/ee/ci/environments/)

[mac stadium gitlab CI](https://about.gitlab.com/blog/2017/05/15/how-to-use-macstadium-and-gitlab-ci-to-build-your-macos-or-ios-projects/)

[Gitlab Predefined variables](https://docs.gitlab.com/ee/ci/variables/predefined_variables.html)


## Reference Code


```yaml

##################################################
# POST DEPLOY
##################################################
# Deploys a App  Debug version of the latest `develop` branch to App Store Connect.
tag_release:
  stage: post_deploy
  needs: ["install:packages"]
  # needs: ["deploy:production"] Need to add back in.
  script:
    - echo "Getting Git Tag version"
    - bundle exec fastlane tag_release
    - git_tag_result=$(bundle exec fastlane display_app_version)
    - git_tag_result=$(echo $git_tag_name | grep "Result:")
		# String subscript range.
    - git_tag_name=${git_tag_result:25}
    - cd SupportTool
    - swift run xvia tag ${git_tag_name} -p
  rules:
    - if: '$CI_COMMIT_BRANCH == "ci/TV-21163-Add-tagging-at-all-layers"'
      when: always
    - if: *is_target_branch_mr_trigger
      when: never
      
```


## Specific Test Case CI

```yaml
  
variables:
	CONFIGURATION:
		value: "debug"
		description: "The build configuration to use throughout the pipeline. Options [`debug`, `release`]. Defaults to `debug`."

	RUNNER_TAG:
		value: "macos"
		description: "Tag for isolating jobs to specific shell runners. Defaults to `macos`. Example, `gitlabrunner-shell2-mac`."


default:
	tags:
		- $RUNNER_TAG
		- 
.test_integration: &test_integration

	- |
	xcodebuild test -quiet \
	-scheme TrackViaNetwork-Package \
	-sdk iphonesimulator15.4 -destination "OS=15.4,name=iPhone 13" \
	-only-testing:"product_nameNetworkIntegrationTests" \
	-skip-testing:"product_nameNetworkIntegrationTests/TableServiceQA3IntegrationTests/testCreateTable" \
	-skip-testing "product_nameNetworkIntegrationTests/TableServiceQA3IntegrationTests/testCreateTableAllFields"


stages:
	- test

run-integration-tests:
	stage: test
	script:
		- echo "Testing the target..."
		- *test_integration
		- echo "Tests complete."
```



## Guides


https://about.gitlab.com/blog/2016/03/10/setting-up-gitlab-ci-for-ios-projects/
https://docs.gitlab.com/runner/configuration/macos_setup.html

https://skofgar.ch/computer-science/2018/11/set-up-gitlab-ci-with-an-ios-project-that-uses-cocoapods/