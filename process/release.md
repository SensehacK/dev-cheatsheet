# Release

## Software Releases

We can make sure to follow Semantic Versioning when it comes to releasing software. Since this is widely accepted standard when it comes to versioning your software package. This definitely helps in estimation and execution when it comes to integration of different packages with different dependencies internally. 

### Tagging

[Git Tagging CLI](tag.md)

### Archiving process


### Logging


## [Packaging](packaging.md)

Architecture support libraries would be different in sizes as it depends on how we are packaging them into the architecture support.
Universal with include `x86 & amd_64` + `arm64`
Internal doc on framework exporting in [iOS / Xcode / Apple ecosystemlibrary/framework#Build%20Output)

[arm64 package 147MB](https://github.com/jgraph/drawio-desktop/releases/download/v22.1.2/draw.io-arm64-22.1.2.dmg)
vs
[dmg universal 217MB](https://github.com/jgraph/drawio-desktop/releases/download/v22.1.2/draw.io-universal-22.1.2.dmg)

## Release Notes

Good release notes could make a big difference compared to just normal bug fixes in every new app version being deployed.


[Examples](https://www.appcues.com/blog/release-notes-examples)

[Smart product updates](https://announcekit.app/blog/5-smart-ways-to-announce-product-updates/)

[Rant changelog](https://piunikaweb.com/2021/06/13/opinion-hey-devs-give-us-proper-update-changelogs-release-notes/)

[John Carmac's Plan archive](https://github.com/ESWAT/john-carmack-plan-archive/tree/master)

## Semantic Versioning

### Apple 

Apple Xcode terminologies with semver

This is the `build` number like version `6.9.420` has been built `9000` times. 

major.minor.bugfix|hotfix (build) = `6.9.420(9000)`

Version = Marketing Version = CFBundleShortVersionString
Build = Current Project Version = CFBundleVersion 

### SPM 

Swift Package manager still doesn't officially support direct version builds.

[SO | spm package version](https://stackoverflow.com/a/62001912/5177704)
