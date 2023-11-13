

# Build Process

This shell script (sh | bash) is a script which runs the xcode project build commands via terminal (CLI)  
You can read on this MAN page of [xcodeBuild](https://keith.github.io/xcode-man-pages/xcodebuild.1.html)


The project can have multiple targets and we specify the scheme which we want to make the CI/CD server run the project.  

### Why Xcode CLI

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

## Resources

[Excellent StackOverflow post about xcode build process related to architecture and linking](https://stackoverflow.com/a/75454378/5177704)

https://en.wikipedia.org/wiki/Instruction_set_architecture


https://www.waldo.com/blog/use-xcodebuild-command-line

https://tarikdahic.com/posts/build-ios-apps-from-the-command-line-using-xcodebuild/