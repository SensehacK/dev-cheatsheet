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

## Optimization

### Debug
During active development, you want to build things fast. It doesn't make sense for you to actively build architectures you don't need to use.

### Release 
While releasing it — for others. Then because you don't want to limit/dictate how they build your app, then you have to build for all possible combinations and make sure your framework compiles for all of them.

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

Great article around how xcode internally handles its stuff for getting more metadata around the project which it needs to make better inferences.
https://pspdfkit.com/blog/2019/how-xcode-indexing-works-and-how-to-solve-problems/

## Resolving arch build errors

`ARCHS`

https://developer.apple.com/documentation/technotes/tn3117-resolving-build-errors-for-apple-silicon

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


## Resources

[Excellent StackOverflow post about xcode build process related to architecture and linking](https://stackoverflow.com/a/75454378/5177704)

https://en.wikipedia.org/wiki/Instruction_set_architecture


https://www.waldo.com/blog/use-xcodebuild-command-line

https://tarikdahic.com/posts/build-ios-apps-from-the-command-line-using-xcodebuild/