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