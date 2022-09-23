# Debugging

## Console Debug

When you have specified the breakpoint and you have llb debugger in the console.

You could use it

> po swift\_variable/ objects

[SO link](https://stackoverflow.com/questions/4735156/xcode-debugger-view-value-of-variable) [Apple Doc](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/debugging_with_xcode/chapters/debugging_tools.html) [Complete Guide](https://andela.com/insights/the-complete-guide-to-debug-swift-code-with-lldb/) [LLDB Debug](https://medium.com/flawless-app-stories/debugging-swift-code-with-lldb-b30c5cf2fd49) [Advanced LLDB](https://medium.com/@fadiderias/xcode-and-lldb-advanced-debugging-tutorial-part-1-31919aa149e0)

## Breakpoint

In UI Xcode IDE, you can specify breakpoints on the code as well group breakpoints, share them and also add specific type of breakpoints. Like having exception breakpoint, printing debug logs, conditional breakpoints.

## Reset Simulator

You can reset the simulator or just uninstall / delete the app from home screen. It is particularly useful for deleting NSUserDefaults & Persistent data associated with the app.

On Simulator App, navigate to ‘Device’ menu -&gt; ‘Reset Content and Settings’

[Link](https://stackoverflow.com/questions/16195859/reset-ios-simulator-application-data-to-run-app-for-first-time)

## Clean Build Folder

If you need to clean the project derived data which can sometimes resolve previous invalid cache of the build system. You can find it in

> Top menu -&gt; Product -&gt; Clean Build Folder


## Change variables in runtime

You can execute commands or change variables while in debugger breakpoint mode in LLDB Xcode console command.


Just enter `expr` or `e` followed by the expression you want to execute.

Function status with parameter change for different user experience timeline switch.
```swift
e NetworkConfigurationManager.shared.setConnectivity(isEnabled: true)
```
Variables alteration
```swift
e isValid = false
```
https://stackoverflow.com/questions/9907387/how-to-change-variables-value-while-debugging-with-lldb-in-xcode