# Travis CI Timeline

While using Travis for Continuos Integration build process, these are my side notes which could help you to grasp better understanding of Travis CI build process timeline.

[Build Timeline](https://travis-ci.com/SensehacK/TravisCI/builds)

## Error 1 Xcode Version Issues

Xcode 10.1 gave one issue of build error with failure rate of 1 / 10. [Describe here](https://github.com/Microsoft/azure-pipelines-tasks/issues/8840)

## Correct config file

XcWorkspace vs XcodeProject, is very important when using cocoaPods dependency pods. [Travis CI \#1](https://travis-ci.com/SensehacK/TravisCI/builds/100396096)

Use shared scheme overall. [Shared Scheme Commit Build Passing](https://travis-ci.com/SensehacK/TravisCI/builds/100202224)

## Error 2 PodFile dependency

Also you can commit podFile. [Travis CI \#2](https://travis-ci.com/SensehacK/TravisCI/builds/100202968) But you need to use XcWorkspace build project command as Travis CI will read "PodFile" & install the dependencies. Thus had Build Failure with error being

`ld: framework not found Pods_TravisCI clang: error: linker command failed with exit code 1 (use -v to see invocation)`

Even I'm not sure what made it fail but I reckon the workspace command not run would be the cause for it.

### CocoaPods Version Differences

Committing podFile-lock would result in build Travis CI failure for me as my local CocoaPods version differed from Travis CI. Local setup had Pre release version. Crosscheck CocoaPods version support for Travis CI as Travis CI supports stable releases of CocoaPods.

Also no need to commit entire Pods folder as it would also increase Git diff loads & more network usage overall. If you need offline dev environment, you could utilize a new branch for "**Offline Env**" Pod setup so everything would work without utilizing internet via "**pod install**" command.

## Error 3 Xcode PodFile References

Also as of now, still haven't committed pods references created by xcodeProject file. \#TODO for me.

\#TODO Update Also committing POD References in xcodeProject file leads to Travis CI build failure. [Travis CI \#3](https://travis-ci.com/SensehacK/TravisCI/builds/100205579)

Reverting the commit makes the build passable again. [Travis CI \#4](https://travis-ci.com/SensehacK/TravisCI/builds/100396096)

Also CocoaPods POD folder doesn't interfere with the build process as far as you assign a workspace according to the project framework.

## Conclusion

Experience with Travis CI with Trial & Error. Learn few things while making it work towards the project with Xcode Test Cases in background.

Work with branches for testing Travis CI or any type of integration for webHooks to instantiate & build the project for any new issues. Keeps the main master branch clean & not dirty when you're in development mode.

