# Build Process

## Intro

This shell script (sh | bash) is a script which runs the xcode project build commands via terminal (CLI)  
You can read on this MAN page of [xcodeBuild](https://keith.github.io/xcode-man-pages/xcodebuild.1.html)


The project can have multiple targets and we specify the scheme which we want to make the CI/CD server run the project.  

## Why Xcode CLI

It is not efficient to open up xcode app (GUI) when trying to work with CI/CD so a headless unit like `xcodeBuild` CLI is recommended which comes preinstalled with Xcode app or you can install them using

```shell
xcode-select --install
```

This installs `Xcode Command Line Tools` when you're opening up xcode setup process for first time. 

## Commands

Lists all the xcode build CLI devices available to run.

```sh
xcrun xctrace list devices
```

## Optimization

### Debug

During active development, you want to build things fast. It doesn't make sense for you to actively build architectures you don't need to use.

### Release 

While releasing it — for others. Then because you don't want to limit/dictate how they build your app, then you have to build for all possible combinations and make sure your framework compiles for all of them.

### Changeset in `.pbxproj` or `.xcodeproj`

This changeset is evident because we updated `iOSDependencySupport` SPM package with new version and also replaced the existing reference in our Xcode target schemes. So new unique identifier is been generated in order to link appropriately. Xcode + SPM cache and build optimization stuff. It internally maintains a graph of frameworks build with linking and what not. So subsequent builds are faster. Xcode maintains that unique tree / graph level ancestry in these files in order to make appropriate optimization necessary and not waste CPU cycle on rebuilding / linking frameworks, assets, libraries. Any resources which require compilation of some sort.

## Binary

Xcode build process will always compile and link the output files in order to run that in machine readable (instructions SET). These usually are called binary files.

Sometimes we want to inspect a binary, you could do this by using this command

```bash
lipo -info <path-to-binary>
```

To be clear, a framework or an app can both be inspected with `lipo`. Similarly if you access the build folder on the simulator, you can inspect the binary as well.

https://llvm.org/docs/CommandGuide/llvm-lipo.html

## Performance

[Xcode performance analysis](performance.md)

## Auto Completion | Indexing | Source LSP

[Great article around how xcode internally handles](https://pspdfkit.com/blog/2019/how-xcode-indexing-works-and-how-to-solve-problems/) its stuff for getting more metadata around the project which it needs to make better inferences.

## Resolving arch build errors

`ARCHS`

[resolving build errors for apple silicon | apple developer](https://developer.apple.com/documentation/technotes/tn3117-resolving-build-errors-for-apple-silicon)

[Apple Silicon and the library incompatibility problem for iOS development](https://susuthapa19961227.medium.com/apple-silicon-and-the-library-incompatibility-problem-for-ios-development-8c2d875283f2)

## Errors

### deployment target mismatch

```log
/code/Project/Carthage/Checkouts/projectName_ios_dependency_one/ProjectDependency_one.xcodeproj: warning: The iOS Simulator deployment target 'IPHONEOS_DEPLOYMENT_TARGET' is set to 10.2, but the range of supported deployment target versions is 11.0 to 16.4.99. (in target 'ProjectDependency_one' from project 'ProjectDependency_one')
** BUILD FAILED **
```
Just open the project in Xcode and set your `Project.xcodeproj` file with `Targets` selected, `General` Tab and `Minimum Deployments` section to the range required by the project.

### clang error building for iOS simulator

```log
ld: in building for iOS Simulator, but linking in object file built for iOS, file `filePath` for architecture arm64

clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

`BuildSettings -> Search -> "Architectures" -> Build Active Architecture Only` 

Comment copied from [apple dev forums](https://developer.apple.com/forums/thread/657913)
I've seen quite a bit of weird behavior with frameworks, I think due to changes to the simulators to support Apple silicon. My temporary workaround is, in my app/extension targets, to add "arm64" to the Excluded Architectures build setting when building for the simulator (as your preview appears to be trying to do), and setting "Build Active Architecture Only" to No for all schemes. Might be worth a try.

### iOS simulator vs iOS vs iOS Rosetta

```sh
Building for 'iOS-simulator', but linking in object file `filepath` built for 'iOS'

Linker command failed with exit code 1 (use -v to see invocation)
```

Switching to iOS physical device or Rosetta simulator fixed it for us.
Basically you can get away by mentioning the `excluded architecture` in your xcode build command.

### Scheme `name` is not currently configured for the test action.

```log
xcodebuild: error: Scheme TestAppUI is not currently configured for the test action.
```

Two approaches 

- Fix the workspace file so the Package is a dedicated scheme.
- Remove the workspace and .xcodeproj files. As far as I can tell, these are just used to run some UI which we never touch. The source files will still be there so we can add them back in the future if we need them.

Reasons

- They introduce multiple schemes which makes isolating the package target/scheme we want to use difficult with `xcodebuild`
- The source files are being left in the repository. Those workspace/proj files were being used to write "UI" around the code, which is not necessary since we rely on the unit tests for CI

### Carthage linking framework issue

TODO: - Clean this logs before committing to the repo.

```log
ld: warning: ignoring duplicate libraries: '-lc++'
ld: warning: search path '/Users/username/git/cloud/project_ios/lib' not found

ld: warning: search path '/Users/username/git/cloud/project_ios/Carthage/Build/iOS/Static/URITemplate.framework' not found

ld: warning: search path '/Users/username/git/cloud/project_ios/lib' not found

ld: warning: search path '/Users/username/git/cloud/project_ios/Carthage/Build/iOS' not found

ld: warning: Could not find or use auto-linked framework 'CoreAudioTypes': framework 'CoreAudioTypes' not found

ld: Undefined symbols:
  (extension in dependency):Swift.Int.init(string: Swift.String) -> Swift.Int?, referenced from:
      projectTestUI.AssetMetadataViewController.(updateMetadata in _B9498481024380D6BB227EFDF8C66DC5)() -> () in AssetMetadataViewController.o
  (extension in dependency):Swift.Collection.subscript.getter : (safe: A.Index) -> A.Element?, referenced from:
      projectTestUI.AssetTableViewController.tableView(_: __C.UITableView, canEditRowAt: Foundation.IndexPath) -> Swift.Bool in AssetViewController.o
      projectTestUI.AssetTableViewController.tableView(_: __C.UITableView, commit: __C.UITableViewCellEditingStyle, forRowAt: Foundation.IndexPath) -> () in AssetViewController.o
  (extension in dependency):Swift.Collection.indicies(containsIndex: A.Index) -> Swift.Bool, referenced from:
      projectTestUI.CustomAssetStore.remove(at: Swift.Int) -> () in CustomAssetStore.o
  static (extension in dependency):Swift.Int32.defaultdependencyTimeScale.getter : Swift.Int32, referenced from:
      projectTestUI.ResumeViewController.(setResumePositionFrom in _8B01A58AC45D5136CBF90D032D54612A)(textField: __C.UITextField) -> Swift.Bool in ResumeViewController.o
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

This got fixed after linking the other SPM framework dependency which had internal `.c` or `.o` library files I believe.
`https://github.com/company-player/iOSPlayerDepSupport`

check its internal dependency just to verify and then clean up and commit.

### rossetta x86_64 | arm64 arch xcode build issues

For some reason xcode doesn't respect the choices for xcode build command being passed around.
Command in test on Xcode 15.0

```sh
xcodebuild -scheme ProjectTest -destination "platform=iOS Simulator,name=iPhone 15,arch=x86_64" build
```

It was selecting the wrong destination, so for some reason the specification of iPhone 15, platform wasn't working as expected.

[Forums suggest using simulator identifier](https://github.com/fastlane/fastlane/issues/21293#issuecomment-1562332624) to mitigate the destination being respect properly.

```sh
xcodebuild -scheme ProjectTest -destination "platform=iOS Simulator,name=iPhone 15,id=2C265EE3-6572-458F-BBD3-98C0285658B0,arch=x86_64" test
```

or 
hard code the architecture settings to `x86_64` to make sure it only runs it on `Rosetta` simulator on M.x arm64 chips.
After doing that you would be granted as this status on CLI

```sh
Build settings from command line:
    ARCHS = x86_64
```

[Bug thread on xcode toolchain, fastlane github](https://github.com/fastlane/fastlane/issues/21293)

### xcode build log file empty

```sh
open /var/folders/fj/1kwwbqhx5r3d0dp1g1fgjwbw0000gn/T/carthage-xcodebuild.dCp7BC.log -a Console
```

Sometimes the log file being generated by `xcode build` command is empty at first when opened using `Console.app`. Wait for few secs depending on your machine's CPU power and it should populate the logs appropriately. Using other text editor doesn't capture the live rendering or output of the logs so its very crucial to open it using `Console.app` in macOS.
[Carthage github empty log issue](https://github.com/Carthage/Carthage/issues/151)




### CoreSimulator is out of date

```log
The version of the CoreSimulator framework installed on this Mac is out-of-date and not supported by this version of Xcode
```

[Apple Dev forums | Fixing CoreSimulator is out of date](https://developer.apple.com/forums/thread/666924?answerId=648561022)

Make sure when you opened the new Xcode version and were you prompted to "install additional components?" if so, click "install" let it install.
And re-run whatever you were trying to achieve.

Or make it explicit run this command

```sh
sudo xcodebuild -runFirstLaunch
```

## Mind Map

[xcode build commands](build_commands.md)

[xcode terminal commands](xcode.md)

## Resources

[Excellent StackOverflow post about xcode build process related to architecture and linking](https://stackoverflow.com/a/75454378/5177704)

[Instruction set architecture](https://en.wikipedia.org/wiki/Instruction_set_architecture)

[use-xcodebuild-command-line](https://www.waldo.com/blog/use-xcodebuild-command-line)

[build-ios-apps-from-the-command-line-using-xcodebuild](https://tarikdahic.com/posts/build-ios-apps-from-the-command-line-using-xcodebuild/)
