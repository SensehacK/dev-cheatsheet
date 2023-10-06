

# Build Process



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


## Performance

[Xcode performance analysis](performance.md)

## Resources

[Excellent StackOverflow post about xcode build process related to architecture and linking](https://stackoverflow.com/a/75454378/5177704)

https://en.wikipedia.org/wiki/Instruction_set_architecture


