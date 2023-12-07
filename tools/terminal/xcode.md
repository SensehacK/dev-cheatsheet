# Xcode

### Checking Xcode SDK Path

Will check whether SDK is linked with path. Command Line tools should be installed and symlinked with path.

```sh
xcrun -k --sdk iphoneos --show-sdk-path
```

### Installing Command Line tools

This command would install the Command line tools on the machine.

```sh
xcrun -k --sdk iphoneos --show-sdk-path
```

### Multiple Xcode Developer tools

If you have multiple versions of the Apple developer tools installed (an Xcode beta, for example), use `xcode-select` to change which version xcode or other build tool uses.