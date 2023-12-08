# Code Checkout

## SSH

Generating the public - private key pair signature for uploading on Git providers online to directly clone repositories without extra input.
Keeps checking out code limited to specific machines rather than the user.

[SSH Passphrase avoidance](https://superuser.com/questions/988185/how-to-avoid-being-asked-enter-passphrase-for-key-when-im-doing-ssh-operatio)

### Test SSH

You can use these commands to test your ssh configuration in the terminal of your choice.

```bash
ssh -T git@github.com
ssh -T git@github.domain.com
```

### Multiple SSH

In your git config file in directory `~/.ssh` you need to open up the `Config` file in a text editor.
Make sure your subdomains and different enterprise accounts have setup properly to get appropriate ssh key configured.

```text
Host *.HOSTNAME
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/_git_p

Host github.subDomain.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/_git_p

Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/github_no_sub_domain
```

### List SSH agents

```bash
ssh-add -l
```

Delete keys agent

```bash
ssh-add -D
```

## Errors

### Terminal prompts disabled

```bash
A shell task (/usr/bin/env git clone --bare --quiet https://github.company.com/project/repo.git /Users/username/Library/Caches/org.carthage.CarthageKit/dependencies/OHHTTPStubs) failed with exit code 128:
fatal: could not read Username for 'https://github.company.com': terminal prompts disabled
```

I was able to solve this by opening a new terminal session and manually `git clone` that url which asked me for `username & password`
For some reason I couldn't use existing ssh option to clone it so I went ahead and created a new personal access token to do this clone.
Carthage config file had 

### Enforced SAML SSO not authorized

```text  
git clone 
failed with exit code 128:
ERROR: The `library-ios' organization has enabled or enforced SAML SSO. To access
this repository, you must use the HTTPS remote with a personal access token
or SSH with an SSH key and passphrase
that has been authorized for this organization.

fatal: Could not read from remote repository.
Please make sure you have the correct access rights
and the repository exists.
```

In order to update the ssh key or personal access token you need to visit `Github` -> Settings and `SSH & GPG keys`.
In that option, you can select `configure SSO` and make the organization you want to access and proceed with authorize option.

## Other Build Errors

### Github old repo Access Issues

```log
github.company.com/lib-ios/Resourcerer.git 
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

Changing Cartfile.private, deleted carthrage resolved file, deleted project cache and build folders.
Changed a dependency branch 
try pointing your NGAuth in the Cartfile to the `ProjectDependency__8.0.0_GHC` branch to this below file.
Cartfile.private

```text
github "https://github.com/company-lib-ios/ProjectDependency.git" "ProjectDependency_8.0.0_GHC"
github "https://github.com/company-lib-ios/OHHTTPStubs" "7.0.0"
```

### xcodebuild path error

```bash
A shell task (/usr/bin/xcrun xcodebuild -project /Users/username/git/github_internal/projectplatform_ios/Carthage/Checkouts/FastCoderFramework/FastCoder.xcodeproj CODE_SIGNING_REQUIRED=NO CODE_SIGN_IDENTITY= CARTHAGE=YES -list) failed with exit code 72:
xcrun: error: unable to find utility "xcodebuild", not a developer tool or in PATH
```

I had to go to `Applications` -> `Xcode` -> `Preferences` -> `Locations` and make sure that `Command Line Tools` is being selected to certain xcode installed version or explicitly select default xcode path in terminal.

Similar thread on [github](https://github.com/XcodesOrg/XcodesApp/issues/254#issuecomment-1210938365) StackOverflow

### tvOS simulator unavailable

```text
Could not find any available simulators for tvOS
```

 `Xcode` -> `Preferences` -> `Platforms`. Install `tvOS` platform and then try it again.

### Archive Failed - code 65

```bash
Build Failed
 Task failed with exit code 65:
 /usr/bin/xcrun xcodebuild -workspace /Users/username/git/github_internal/projectplatform_ios/Carthage/Checkouts/OHHTTPStubs/OHHTTPStubs/OHHTTPStubs.xcworkspace -scheme OHHTTPStubs\ Mac\ Framework -configuration Release -derivedDataPath /Users/username/Library/Caches/org.carthage.CarthageKit/DerivedData/14.3_14E222b/OHHTTPStubs/7.0.0 ONLY_ACTIVE_ARCH=NO CODE_SIGNING_REQUIRED=NO CODE_SIGN_IDENTITY= CARTHAGE=YES archive VALIDATE_WORKSPACE=NO -archivePath /var/folders/2k/9fdzvdzx13nfcvq2p27r3zsc0000gp/T/OHHTTPStubs SKIP_INSTALL=YES GCC_INSTRUMENT_PROGRAM_FLOW_ARCS=NO CLANG_ENABLE_CODE_COVERAGE=NO STRIP_INSTALLED_PRODUCT=NO (launched in /Users/username/git/github_internal/projectplatform_ios/Carthage/Checkouts/OHHTTPStubs)

This usually indicates that project itself failed to compile. Please check the xcodebuild log for more details: /var/folders/2k/9fdzvdzx13nfcvq2p27r3zsc0000gp/T/carthage-xcodebuild.UgRayH.log
```

Checking the logs it shows 

```bash
-o /Users/username/Library/Caches/org.carthage.CarthageKit/DerivedData/14.3_14E222b/OHHTTPStubs/7.0.0/Build/Intermediates.noindex/ArchiveIntermediates/OHHTTPStubs\ Mac\ Framework/IntermediateBuildFilesPath/OHHTTPStubs.build/Release/OHHTTPStubs\ Mac\ Framework.build/Objects-normal/x86_64/Binary/OHHTTPStubs
ld: file not found: /Applications/Xcode-14.3.0.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/lib/arc/libarclite_macosx.a
clang: error: linker command failed with exit code 1 (use -v to see invocation)

/Users/username/git/github_internal/projectplatform_ios/Carthage/Checkouts/OHHTTPStubs/OHHTTPStubs/OHHTTPStubs.xcodeproj: warning: The macOS deployment target 'MACOSX_DEPLOYMENT_TARGET' is set to 10.9, but the range of supported deployment target versions is 10.13 to 13.3.99. (in target 'OHHTTPStubs Mac Framework' from project 'OHHTTPStubs')
** ARCHIVE FAILED **


The following build commands failed:
 Ld /Users/username/Library/Caches/org.carthage.CarthageKit/DerivedData/14.3_14E222b/OHHTTPStubs/7.0.0/Build/Intermediates.noindex/ArchiveIntermediates/OHHTTPStubs\ Mac\ Framework/IntermediateBuildFilesPath/OHHTTPStubs.build/Release/OHHTTPStubs\ Mac\ Framework.build/Objects-normal/x86_64/Binary/OHHTTPStubs normal x86_64 (in target 'OHHTTPStubs Mac Framework' from project 'OHHTTPStubs')
(1 failure)

```

### Xcode SSH Git dependency

```bash
  

**Showing Recent Issues**

x-swift-package-repository-authentication://?scm=com.apple.dt.Xcode.sourcecontrol.Git&url=git@github.com:company-aae-ios/CIMHAL.git#error=-1004&fingerprint=A764003173480B54C96167883ADB6B55CF7CFD1D415055AEDFF2E2C8A8147D03: Server SSH Fingerprint Failed to Verify
```

Just verify it properly and trust the server.

### Credentials are wrong or missing

```bash
FastCoderFramework

x-swift-package-repository-authentication://?scm=com.apple.dt.Xcode.sourcecontrol.Git&url=https://github.com/company-aae-ios/FastCoderFramework.git#error=-1005: github.com: Authentication failed because the credentials were missing

Fetching from https://github.com/company-aae-ios/FastCoderFramework.git
skipping cache due to an error: Authentication failed because the credentials were missing
skipping cache due to an error: Authentication failed because the credentials were missing
```

It seems the problem is three fold. 
Xcode previous issues with SSH -> RSA rather than the latest `ED` algorithm key generation

On terminal it properly clones the URL which is erroring out so it is using `ssh` appropriately.
and I can't explicitly change the url from https to ssh - I can with `gitconfig`  - `insteadOf` rule but not clean way of doing it for now.

third: 
Github `fine grain tokens` needs to get access to organization repos and I believe the organization have disabled this to an extent as per this [issue thread](https://github.com/orgs/community/discussions/40910)

I'll try the classic way of github token generation.
Voila Classic github token works and it enabled to download the repo.

### library Path update

ProjectDependency_v7.3.0 vs

```log
github "https://github.com/company-name/ProjectDependency.git" "ProjectDependency_8.0.0_GHC"
```

### error: pathspec '' did not match any file(s) known to git

```log
A shell task (/usr/bin/env git checkout --quiet --force v2.0.0 (launched in /Users/builder/Library/Caches/org.carthage.CarthageKit/dependencies/dependencyName)) failed with exit code 1:
error: pathspec 'v2.0.0' did not match any file(s) known to git
```

This was due to I cloned a repository in its new destination, but the tags are present locally not remotely. So mostly I have to push new tags or existing tags to the remote git repo.
