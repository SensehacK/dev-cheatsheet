# Build Process

## Intro

This shell script (sh | bash) is a script which runs the xcode project build commands via terminal (CLI)  
You can read on this MAN page of [xcodeBuild](https://keith.github.io/xcode-man-pages/xcodebuild.1.html)

The project can have multiple targets and we specify the scheme which we want to make the CI/CD server run the project.  

Information for `xcodebuild`, `xcrun` & `swift`
Copied off [SO post](https://stackoverflow.com/a/69030619) 

## xcodebuild

`xcodebuild` is part of Xcode's bundled command-line tools package. From the [manpages](http://www.manpagez.com/man/1/xcodebuild/):

> build Xcode projects and workspaces
> 
> xcodebuild builds one or more targets contained in an Xcode project, or builds a scheme contained in an Xcode workspace or Xcode project.

`xcodebuild` has lots of options and use cases. The options are equivalent to certain user actions within the Xcode IDE. Example usage:

```swift
xcodebuild -workspace MyWorkspace.xcworkspace -scheme MyScheme
```

> Builds the scheme MyScheme in the Xcode workspace MyWorkspace.xcworkspace.

In the command above, we build the workspace without Xcode, using what Xcode runs internally for compilation. Xcode can only be installed on macOS and we have the same limitations for using its command-line tools, including `xcodebuild` and `xcrun`.

## xcrun

`xcrun` is another Xcode command-line tool part of Xcode's CLI tools. From the [manpages](http://www.manpagez.com/man/1/xcrun/):

> run or locate development tools
> 
> `xcrun` provides a means to locate or invoke coexistence- and platform-aware developer tools from the command-line, without requiring users to modify makefiles or otherwise take inconvenient measures to support multiple Xcode toolchains.

```swift
xcrun [-sdk SDK] -find <tool_name>
```

`xcrun` is also commonly used with `Xcode-select` to manage multiple Xcode versions on the same machine. Every version of Xcode comes bundled with its own development tools, and we can use `xcrun` to get the current path to them:

```swift
xcrun xcode-select --print-path
```

## swift

`swift` is the Swift REPL. `swift` is a command-line tool that includes the Swift toolchain but can also be installed outside of the Xcode bundled tools. `swift` is different from `xcodebuild` and `xcrun` because it is compiled Swift rather than C. `swift` is not well documented in the MacOS [manpages](http://www.manpagez.com/man/1/swift/) documentation, however, Apple has documented these tools on its [blog](https://developer.apple.com/swift/blog/?id=18):

> Xcode 6.1 introduces yet another way to experiment with Swift in the form of an interactive Read Eval Print Loop, or REPL.

## Mind Map

[xcode build commands](build_commands.md)

[xcode terminal commands](xcode.md)

[xcode performance analysis](performance.md)

## Why Xcode CLI

It is not efficient to open up xcode app (GUI) when trying to work with CI/CD so a headless unit like `xcodeBuild` CLI is recommended which comes preinstalled with Xcode app or you can install them using

```shell
xcode-select --install
```

This installs `Xcode Command Line Tools` when you're opening up xcode setup process for first time. 

## Commands

### List build devices

Lists all the xcode build CLI devices available to run.

```sh
xcrun xctrace list devices
```

### Which Xcode version

```sh
xcodebuild -version
```

### Swift version

```sh
xcrun swift -version
```

### Command line tools version

```sh
gcc --version

```

### Inspecting Binary

Xcode build process will always compile and link the output files in order to run that in machine readable (instructions SET). These usually are called binary files.

Sometimes we want to inspect a binary, you could do this by using this command

```bash
lipo -info <path-to-binary>
```

To be clear, a framework or an app can both be inspected with `lipo`. Similarly if you access the build folder on the simulator, you can inspect the binary as well.
[llvm | lipo guide](https://llvm.org/docs/CommandGuide/llvm-lipo.html)

## Optimization

### Debug

During active development, you want to build things fast. It doesn't make sense for you to actively build architectures you don't need to use.

### Release 

While releasing it — for others. Then because you don't want to limit/dictate how they build your app, then you have to build for all possible combinations and make sure your framework compiles for all of them.

### Changeset in `.pbxproj` or `.xcodeproj`

This changeset is evident because we updated `iOSDependencySupport` SPM package with new version and also replaced the existing reference in our Xcode target schemes. So new unique identifier is been generated in order to link appropriately. Xcode + SPM cache and build optimization stuff. It internally maintains a graph of frameworks build with linking and what not. So subsequent builds are faster. Xcode maintains that unique tree / graph level ancestry in these files in order to make appropriate optimization necessary and not waste CPU cycle on rebuilding / linking frameworks, assets, libraries. Any resources which require compilation of some sort.





## Auto Completion | Indexing | Source LSP

[Great article around how xcode internally handles](https://pspdfkit.com/blog/2019/how-xcode-indexing-works-and-how-to-solve-problems/) its stuff for getting more metadata around the project which it needs to make better inferences.

## Resolving arch build errors

`ARCHS`

[resolving build errors for apple silicon | apple developer](https://developer.apple.com/documentation/technotes/tn3117-resolving-build-errors-for-apple-silicon)

[Apple Silicon and the library incompatibility problem for iOS development](https://susuthapa19961227.medium.com/apple-silicon-and-the-library-incompatibility-problem-for-ios-development-8c2d875283f2)


## ssh Binaries

You can solve this problem in three ways

- netrc + scmProvider (xcodebuild)
- Git config `insteadOf` rule override
- keychain override

#### netrc_scmProvider

```
I did a few things:  

-  moved the keychain out of ~/Library
- put github credentials in a ~/.netrc file
- told xcodebuild to use the netrc: `-scmProvider system -packageAuthorizationProvider netrc`

Basically because the URL has [github.com](http://github.com/) in it, xcode wants to know what credentials are needed to get it, even if the URL is not private. This all works around that so that Xcode doesn't need to ask. It was hanging because ti was waiting to be provided with creds and no one is there to fill in the dialog.
```


Basically you can utilize xcode build system to appropriately ask them to use ssh agent and `.netrc` configs to get around this problem

Copied below stuff for archival purposes
[swift | forums | Support for resolving private packages through HTTPS with xcodebuild](https://forums.swift.org/t/support-for-resolving-private-packages-through-https-with-xcodebuild/48581/7)

```log
If you use `xcodebuild -scmProvider xcode`, HTTPS can be used, but you would typically log in via Xcode preferences to your SCM service account.
Looks like there is no alternative to using the Xcode UI today, so you would need to login once via that on the CI machine to store the credentials and then using `xcodebuild -scmProvider xcode` should be able to use those credentials you configured.
```

#### gitconfig_insteadOf

For us using the netrc file does the trick. But note that besides:

```swift
machine github.com
  login <username>
  password <personal access token>
```

You also need to add this if your Package.swift points to binaries stored in GitHub package registry:

```swift
machine maven.pkg.github.com
  login <username>
  password <personal access token>
```

Took me quite a while to figure this out, but sub domains are not included in the machine definitions, so specify them individually


#### keychain_override

[aws | troubleshooting artifact downloading docs](https://docs.aws.amazon.com/codeartifact/latest/ug/swift-troubleshooting.html#swift-troubleshooting-ci-machine)

[github issue | keychain token option](https://github.com/swiftlang/swift-package-manager/issues/7236)


## [Build Errors](build_errors.md)

## Resources

[Excellent StackOverflow post about xcode build process related to architecture and linking](https://stackoverflow.com/a/75454378/5177704)

[Instruction set architecture](https://en.wikipedia.org/wiki/Instruction_set_architecture)

[use-xcodebuild-command-line](https://www.waldo.com/blog/use-xcodebuild-command-line)

[build-ios-apps-from-the-command-line-using-xcodebuild](https://tarikdahic.com/posts/build-ios-apps-from-the-command-line-using-xcodebuild/)
