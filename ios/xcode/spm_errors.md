# SPM Errors

## Module Cache Path 
When you changed the whole package name & folder. Xcode clean build doesn't work sometimes when you run `swift run package_name` on Command Line.
So delete the `.build` directory.
[PCH was compiled with module cache path error](https://stackoverflow.com/questions/57080473/pch-was-compiled-with-module-cache-path-error)


## Packages Not downloaded

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

### missing required module

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
```sh
git@github.com:repoName/project.git: An unknown error occurred. reference 'refs/remotes/origin/develop' not found (-1)
```

You can have this error sometimes if you're having Xcode local package name conflicting with similar remote package name. So one way to get past this error is to do `Xcode` -> `File` -> `Packages` ->  `Reset Package Cache`

This could be resolved by deleting the project `Packaged.resolved` files and removing the resolved package references and if that doesn't work deleting the SPM manifest cache libraries. 
And if it still doesn't work might as well `Reset Package Cache` in Xcode menu bar and then `Resolve Package Versions`. If this fails might as well update your dependencies to see if something changed on the server with old tagged versions by using `Update to Latest versions` should do the trick. If all fails restart mac and refer to the `Notes` section of this document.

& all of it doesn't work or you want selective cache deletion navigate to [[#skipping cache]]

## skipping cache

```sh
skipping cache due to an error: git@github.com:org/proj-name.git: An unknown error occurred. reference 'refs/remotes/origin/develop' not found (-1)
```

This happens due to multiple caches and some issues with `ssh:` dependencies

> I think I may have found the issue here! After a ton of digging it seems Xcode and Swift PM has a bug with repos using git@ rather than https://
> Using ssh we are getting a hanging ref to remote/origin/main in our caches and derived data

[Good SO | Post](https://stackoverflow.com/a/74130700/5177704)

```sh
# Create the file & give appropriate permissions
chmod +x fix-spm-cache.sh

# In your project directory
./fix-spm-cache.sh project-name
```
`fix-spm-cache.sh` contents copied from the post

```sh
#!/bin/bash
if [[ $# -eq 0 ]] ; then
    echo 'Please call the script with the name of your project as it appears in the derived data directory. Case-insensitive.'
    echo 'For example: ./fix-spm-cache.sh myproject'
    exit 0
fi

# Delete all directories named "remotes" from the global Swift Package Manager cache.
cd ~/Library/Caches/org.swift.swiftpm/repositories
for i in $(find . -name "remotes" -type d); do
    echo "Deleting in SPM Cache: $i"
    rm -rf $i
done

# Find derived data directories for all projects matching the script argument, and
# delete all directories named "remotes" from source package repositories cache for those projects. 

cd ~/Library/Developer/Xcode/DerivedData/
for project in $(find . -iname "$1*" -type d -maxdepth 1); do
    for i in $(find "$project/SourcePackages/repositories" -name "remotes" -type d); do
        echo "Deleting in DerivedData: $i"
        rm -rf $i
    done
done
```

### Package.resolved file is corrupted or malformed

[SO | package resolved file is corrupted](https://stackoverflow.com/questions/67185817/package-resolved-file-is-corrupted-or-malformed)

Had to reset the xcode 15.3 with appropriate versioning "originHash" : 

```log
Package.resolved file is corrupted or malformed; fix or delete the file to continue: unknown 'PinsStorage' version '3' at '/Users/username/actions-runner/_work/proj_fold/proj/proj_name.xcodeproj/project.xcworkspace/xcshareddata/swiftpm/Package.resolved'.
```

Switching back from version 3 to version 2 worked fine for me. Maybe not committing the `Package.resolved` file should be more important to avoid these kind of flaky build failures.
Since on CI we use Xcode 15 and on my local machine I upgraded to 15.3 recently which led to upgrade of Package.resolved file with appropriate new keys like 
`originHash` & `version upgrade` to 3.

### Build input file cannot be found

```error

Build input file cannot be found: '/Users/ksave9wrwa57/git/cloud/saf/Sources/werw/Events and Reporting/PlaySpsaan.swift'. Did you forget to declare this file as an output of a script phase or custom build rule which produces it?
```



### Credentials were rejected

```log
Showing All Messages skipping cache due to an error: Authentication failed because the credentials were rejected
```

This may happen due to one of these few reasons.

- Xcode cache is not updated. Please force quit your xcode and try again. Resolving stuff.

- Was able to clone personal repos of the account but not other organization. Turns out my firefox browser session was improperly interrupted while not completing the `allow SSO` for the independent organizations mention over here.  [github token creation SSO](git/token#SSO)

- Your local system macOS keychain could have conflicting secure tokens stored for your specific domain, subdomain github flavor of version. This could happen because you have multiple git credentials, multiple git clients like Github desktop, git CLI, Gitkraken, git VSCode etc.

- Your git config `.dotFiles` found under your root personal account directory like `~` or `~/.ssh/` or your personalized config. check the file `config` for specific git configuration being setup on a global level. Sometimes you can have specific sub-directories rules or host rules. Specified over [git config global](git/config#Global) 



- Make sure it has `.git` full repo URL.
```bash
https://github.com/apple/swift-argument-parser.git
```

- Update global git config from `ssh` to `https` & try again.

#### Minor Rant

So get this - remember the global git config rule. that was necessary for previous xcode since apple for some reason couldn't support GitHub fine grain tokens. -> all right I get it apple isn't on cutting edge of technology. I do `classic token` problem solved right?  
No it had a problem with the `ssh` key - value pair algorithm - it can just accept the latest and greatest ED11342 xxx till last Xcode 15 beta or something 5 months back.  
So had to revert to a 160 bit or something inferior encryption ssh method.Now fast forward to 2024 - we are all good and the project is great & it now fails before we upgraded the IOS dependency layer (SPM) which takes in latest helio and other stuff being bumped according to SEMVER. All good but now the SPM cache is invalidated. guess what we have been running on `cache` for past 3 - 4 months because well we were more hot on Nitro stuff innit & PP just had minor releases - cache worked fine.Now for some innate reason - apple | xcode can't take the latest token provided by us and dare u the old token is valid. On top of it xcode creates 3 more entries in keychain (password manager) to store the same tokens for maybe individual UUID projects (why - prolly a bug) which we cant even track since there isn't an open radarr bug tracking system provided by apple.  
Now I thought maybe previously we had to revert on `ssh` from https. This time I'll revert back this since its `Classic -apple` yk - one day it works - other day it breaks. & Voila it freaking works again.  
cue the meme


I had to disable HTTPS to SSH rewriting for Git.
`~/.gitconfig` file

```config
[url "git@github.com:"]
    insteadOf = https://github.com/
```

yeah - somewhere along the lines, xcode does its own gymnastics when cloning repo via SPM vs normal other processes like carthage / cocoapods.  
I reckon it hit a snag when it was not able to understand which to take when using SPM & hence previously it was just taking references from cache. Now since our old project system is intertwined with 2 build systems we have overall made it worse for xcode. But there's no documentation from apple about this behavior. This issue isn't reproducible on newer project cuz it uses SPM (first party)

Xcode seems to not like ed25519 encrypted ssh keys. Try removing those, and replace with rsa keys instead - Xcode 14.x

[Similar thread | SPM xcodebuild commands (resolve dependencies) run from AppCode do not use Xcode accounts](https://youtrack.jetbrains.com/issue/OC-21826)



### 

```sh
Package manifest at '/Package.swift' cannot be accessed (/Package.swift doesn't exist in file system)
```

this was happening while attempting to checkout a SPM dependency at a version that didn't yet have a Package.swift

[Package manifest | SO](https://stackoverflow.com/questions/75473774/package-manifest-at-package-swift-cannot-be-accessed-package-swift-doesnt)