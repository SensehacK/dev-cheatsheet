# Crash


## Constraints

```log
libc++abi.dylib: terminating with uncaught exception of type NSException
*** Terminating app due to uncaught exception 'NSInternalInconsistencyException', reason: 'Modifications to the layout engine must not be performed from a background thread after it has been accessed from the main thread.'
terminating with uncaught exception of type NSException
CoreSimulator 757.5
```



## Xcode

### Build linking error
ld: in /Users/ksave/Projects/product_name-iOS/Pods/Realm/core/librealmcore-ios.a(array_binary.o), building for iOS Simulator, but linking in object file built for iOS, for architecture arm64
clang: error: linker command failed with exit code 1 (use -v to see invocation)