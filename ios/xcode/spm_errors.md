## Errors

### Module Cache Path 
When you changed the whole package name & folder. Xcode clean build doesn't work sometimes when you run `swift run package_name` on Command Line.
So delete the `.build` directory.
[PCH was compiled with module cache path error](https://stackoverflow.com/questions/57080473/pch-was-compiled-with-module-cache-path-error)


### Packages Not downloaded

```log
Not able to download packages properly.
```

Option in Menu bar.
Xcode ->  File -> Packages -> 
`Reset package caches`
& even not working then select `resolve packages`

### Artifact not mapped with Binary Target

```log
Binary target 'LibraryName' could not be mapped to an artifact with the expected name 'LibraryName'
```

Deleting `~/Library/org.swift.swiftpm` helped for us

```sh
rm -rf ~/Library/org.swift.swiftpm
```

[Apple dev thread](https://developer.apple.com/forums/thread/711597)

```log
**security-spm-client-manifest**

Revision 37351b7ac065f11cd70c41ca7610539a82856ddf for security-spm-client-manifest remoteSourceControl https://github.company.com/contentsecurity/security-spm-client-manifest.git version 7.3.5 does not match previously recorded value 00a34dfabec0d11baebsafasfce96793e984a8b

Fetching from https://github.company.com/contentsecurity/security-spm-client-manifest.git (cached)
```

### missing required module ''

```bash
<unknown>:0: error: missing required module 'HLSObjectiveC'
```

*This* usually happens if the target / library sources have an import product_name / library and you haven't defined its dependency in the `target` package.swift

```swift
// Logging.swift
import productName

// Package.swift
.target(
	name: "Logging",
	dependencies: [.product(name: "productName",
							package: "packageName")],
	path: "Sources/Logging"
)
```

### `Missing package product <package name>`

Just run the xcode build command with a flag 

```sh
xcodebuild -resolvePackageDependencies
```

[spm | missing-package-product](https://blog.leonifrancesco.com/articles/missing-package-product)

Xcode GUI approach to get past this error is to do `Xcode` -> `File` -> `Packages` ->  `Reset Package Cache`
Also this kinda relates to `reference 'refs/remotes/origin/' not found (-1)` just below and I also added to do `Update to Latest Versions` in order for missing package products to properly link for iOS Simulator builds.

[Another source](https://swiftylion.com/articles/missing-package-product) 

Another solution I tried was opening up the local SPM Package which has recently been divided into three modules / packages. So maybe the `.xcodeProj` was having difficulty picking that up appropriately. I manually build all the schemes again & open the `.xcodeProj` file again & this time it didn't have this issue with Missing package product.
 
### failed downloading required by target

```log
failed downloading 'https://artifactory.website.com/someLibrary.zip' which is required by binary target 'target_name': Operation cancelled

downloadError("The network connection was lost.")
```

Sometimes your vpn or internet connection is too slow, better way to debug is just copy the URL and check if we are getting the asset being downloaded at appropriate speeds in your browser or curl. Turns out I was on really bad  Wifi network which was throttling my speed and xcode SPM was just showing me loading circle for past 5 minutes without any progress bar to explain how much percentage was being done or at what speeds.

### long time fetching packages

Sometimes your SAML or 2FA is not updated so that kinda makes the `fetching packages` load continuously on Xcode to update the library dependencies.
So make sure your VPN or 2FA is signed in properly since it was not proceeding further to check out the code with updated version.

### parsing package manifest failed

```log
Invalid semantic version string 'branch_name`
```

This was due to using branch name where tag semantic version was needed. Build error for SPM package.swift where the syntax should be 

```swift
.package(url: "git@github.com:repoName/project.git", from: "0.1.0"),
.package(url: "git@github.com:repoName/project.git", branch: "develop"),
```

### reference 'refs/remotes/origin/' not found (-1)

skipping cache due to an error
```log
git@github.com:repoName/project.git: An unknown error occurred. reference 'refs/remotes/origin/develop' not found (-1)
```

This could be resolved by deleting the project `Packaged.resolved` files and removing the resolved package references and if that doesn't work deleting the SPM manifest cache libraries. 
And if it still doesn't work might as well `Reset Package Cache` in Xcode menu bar and then `Resolve Package Versions`. If this fails might as well update your dependencies to see if something changed on the server with old tagged versions by using `Update to Latest versions` should do the trick. If all fails restart mac and refer to the `Notes` section of this document.


### Package.resolved file is corrupted or malformed

[SO | package resolved file is corrupted](https://stackoverflow.com/questions/67185817/package-resolved-file-is-corrupted-or-malformed)

Had to reset the xcode 15.3 with appropriate versioning "originHash" : 

```log
Package.resolved file is corrupted or malformed; fix or delete the file to continue: unknown 'PinsStorage' version '3' at '/Users/username/actions-runner/_work/proj_fold/proj/proj_name.xcodeproj/project.xcworkspace/xcshareddata/swiftpm/Package.resolved'.
```

Switching back from version 3 to version 2 worked fine for me. Maybe not committing the `Package.resolved` file should be more important to avoid these kind of flaky build failures.
Since on CI we use Xcode 15 and on my local machine I upgraded to 15.3 recently which led to upgrade of Package.resolved file with appropriate new keys like 
`originHash` & `version upgrade` to 3.