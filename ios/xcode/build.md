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

### List build devices

Lists all the xcode build CLI devices available to run.

```sh
xcrun xctrace list devices
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




## Mind Map

[xcode build commands](build_commands.md)

[xcode terminal commands](xcode.md)

[xcode performance analysis](performance.md)

## Auto Completion | Indexing | Source LSP

[Great article around how xcode internally handles](https://pspdfkit.com/blog/2019/how-xcode-indexing-works-and-how-to-solve-problems/) its stuff for getting more metadata around the project which it needs to make better inferences.

## Resolving arch build errors

`ARCHS`

[resolving build errors for apple silicon | apple developer](https://developer.apple.com/documentation/technotes/tn3117-resolving-build-errors-for-apple-silicon)

[Apple Silicon and the library incompatibility problem for iOS development](https://susuthapa19961227.medium.com/apple-silicon-and-the-library-incompatibility-problem-for-ios-development-8c2d875283f2)

## [Build Errors](build_errors.md)

## Resources

[Excellent StackOverflow post about xcode build process related to architecture and linking](https://stackoverflow.com/a/75454378/5177704)

[Instruction set architecture](https://en.wikipedia.org/wiki/Instruction_set_architecture)

[use-xcodebuild-command-line](https://www.waldo.com/blog/use-xcodebuild-command-line)

[build-ios-apps-from-the-command-line-using-xcodebuild](https://tarikdahic.com/posts/build-ios-apps-from-the-command-line-using-xcodebuild/)
