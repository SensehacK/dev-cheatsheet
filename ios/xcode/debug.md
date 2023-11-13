# Debugging

## Console Debug

When you have specified the breakpoint and you have llb debugger in the console.

You could use it

```llvm
po swift\_variable/ objects
```

[SO link](https://stackoverflow.com/questions/4735156/xcode-debugger-view-value-of-variable) [Apple Doc](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/debugging_with_xcode/chapters/debugging_tools.html) [Complete Guide](https://andela.com/insights/the-complete-guide-to-debug-swift-code-with-lldb/) [LLDB Debug](https://medium.com/flawless-app-stories/debugging-swift-code-with-lldb-b30c5cf2fd49) [Advanced LLDB](https://medium.com/@fadiderias/xcode-and-lldb-advanced-debugging-tutorial-part-1-31919aa149e0)

## Breakpoint

In UI Xcode IDE, you can specify breakpoints on the code as well group breakpoints, share them and also add specific type of breakpoints. Like having exception breakpoint, printing debug logs, conditional breakpoints.

## Print Memory address

Object Reference types
```swift
print(Unmanaged.passUnretained(someVar).toOpaque())
```

Sequence Value types memory address
```swift
let array1 = [1,2,3]
    let array2 = array1
    array1.withUnsafeBufferPointer { (point) in
        print(point)
    }
```

Structs memory address
```swift
struct CustomType { let name = "Hello" }
let firstObject = CustomType()
withUnsafePointer(to: firstObject) { print("\($0)") }
```

Custom conditions in breakpoints 
https://developer.apple.com/documentation/xcode/setting-breakpoints-to-pause-your-running-app

[SO](https://stackoverflow.com/questions/24058906/printing-a-variable-memory-address-in-swift)
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


## Debug  Prints

Your object can conform to protocol `CustomDebugStringConvertible` in order to print your custom debug message prints.

Whenever you use `debugPrint(_:)` or `String(reflecting:)` 

Having it in an extension is a good practice since it improves readability and doesn't clutter up your main implementation layer or business layer. 

```swift
extension CustomClassOrStruct: CustomDebugStringConvertible {
    var debugDescription: String {
        return "(\(self.property1), \(self.property2))"
    }
}
```


https://developer.apple.com/documentation/swift/customdebugstringconvertible

## View Debugging


Xcode provides us a great way to visually debug a view being presented on the screen.

But to top it off with the icing on the cake you can actually change constraints or values of the paused debugged view.
`lldb` is pretty powerful in most cases to let us change values on the fly and get more testing while in the current state and saves us a lot of time to recreate that current state again by relaunching the app. Which I would admit that's how I usually do my UI testing previously with constraints. But with `lldb` you can just change specific constraints values by executing `expression constraint_memory_pointer.value = newValue`

```swift
// 1 Change UI element with new value
expression constraint_memory_pointer.value = newValue 

// 2 Retrigger UI Draw Cycle / Refresh UI
expr CATransaction.flush()

// 3 Executing in swift environment
expression -l Swift -O --
```



If you get errors of `unresolved identifier` you may have to import UIKit, Appkit or any UI dependent Cocoa library of apple ecosystem you're debugging. Refer this below article for more insights.

https://itnext.io/leveraging-swift-in-xcodes-lldb-d75e2adc5741

Objective C variant of this code 
https://medium.com/ios-os-x-development/dynamically-modify-ui-via-lldb-expression-1b354254e1dd

You can definie lldb alias'es just like how you add them for your zShell or bash shell. It is located at `~/.lldbinit` directory of the root of OS. 

A shared lldb alias config file from the above sourced link 
```bash
command alias objc expression -l objc -O --

command regex swift 's#(.+)#expression -l Swift -O -- defer { CATransaction.flush() }; %1#'

breakpoint set -n AppDelegate.application --one-shot true --auto-continue true

breakpoint command add

swift import Foundation

swift import UIKit

swift import MyApp_tvOS

swift import MyApp_iOS

swift func $printSubviews(of view: UIView) { print(view.perform("recursiveDescription")!) }

swift func $findViews<C: UIView>(_ c: C.Type, in t: UIView = UIApplication.shared.keyWindow!) -> [C] { var r: [C] = []; t.subviews.forEach({ if let v = $0 as? C { r.append(v) }; r.append(contentsOf: $findViews(C.self, in: $0)) }); return r }

swift func $flush() { CATransaction.flush() }

swift func $view<T>(_ x: T) -> UIView { unsafeBitCast(x, to: UIView.self) }

swift func $vc<T>(_ x: T) -> UIViewController { unsafeBitCast(x, to: UIViewController.self) }

swift func $nav<T>(_ x: T) -> UINavigationController { unsafeBitCast(x, to: UINavigationController.self) }

swift extension NSObject { static func $from(_ addr: UInt) -> Self { unsafeBitCast(addr, to: Self.self) }}

DONE
```
[git gist](https://gist.github.com/maxchuquimia/3eb255b0ea2088829b460358d9f058d3)


## Method_Swizzling


You can reverse engineer certain libraries / frameworks of apple UIKit , AppKit and utilize objective-C runtime methods to quickly replace our own implementation of the method we want to override.
Sometimes the library we are consuming won't expose all the options to tweak or change its behavior so method swizzling basically comes into the picture where you just hack / capture the memory and replace it with our own custom function / method. To get more custom behavior and just understand the underlying working architecture of the abstracted library.

Haven't heard anyone explicit mention this most of the time but one senior engineer from Objective - C did gave me a nudge to check it out in 2020 just because I mentioned I came from Turbo-C , DosBox and C++ compilers era.
