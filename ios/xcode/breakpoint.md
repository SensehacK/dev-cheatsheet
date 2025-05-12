# Breakpoint

## IDE

In UI Xcode IDE, you can specify breakpoints on the code as well group breakpoints, share them and also add specific type of breakpoints. Like having exception breakpoint, printing debug logs, conditional breakpoints.

[Apple dev | Stepping through code and inspecting variables to isolate bugs](https://developer.apple.com/documentation/xcode/stepping-through-code-and-inspecting-variables-to-isolate-bugs)

## Manual

Debugger breakpoint in code

```swift
func fail(desc: String) {
  #if DEBUG
    print("assertFail:\(desc)")
    raise(SIGINT)
  #endif
}
```
[SO | Post](https://stackoverflow.com/a/37181180/5177704)


## breakpoint disabled

For me on Xcode beta 16 and 15 it automatically just disables when I'm using a unit test breakpoints.
[SO | xcode breakpoints stop working](https://stackoverflow.com/questions/64790/why-arent-xcode-breakpoints-functioning)

[apple dev forum | thread](https://forums.developer.apple.com/forums/thread/744108?answerId=776446022#776446022)


```sh
Product>Scheme>Edit scheme>..
Under Run>info>Executable check "Debug executable"
```

Deleting my build folder and restarting Xcode also helped.
Sometimes I had issues if my iOS physical device was running a beta version and on a new major OS (iOS 17 Xcode) but running (iOS 18 beta 4x)
So maybe its still building the debug symbols or cache for the new OS.
