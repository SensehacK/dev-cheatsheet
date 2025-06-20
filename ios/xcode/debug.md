# Debugging


## Basic Remediation

> Have you tried turning it OFF and ON again - The IT Crowd

Glad I can reference that British TV show in my work - hobby - mind map knowledge base.

The number of times an iOS Engineer has to go back to basics things to try while having a build or runtime error from Xcode - Apple Developer Tools.

- Manually clearing out Derived Data
- Clean Build Folder
- Deleting app on simulator
- Closing Xcode
- Force quitting Xcode
- Swift Package Manager - Reset package cache
- SPM - resolving packages
- Restarting Mac



## Finding the culprit

Open the `.log` file on `console.app` and make sure to not take the last error stack trace at its face value. 
Always back track to a point where you can see the actual error.
When Xcode build command fails on GUI or CLI. CLI is a little bit tricky and can only provide final failure information of below logs. 

```sh
** BUILD FAILED **
** ARCHIVE FAILED **
** TEST FAILED **
```

You can solve this problem two ways 

1. Open the file / error project target scheme product file in question on Xcode GUI. After Xcode 14 updates, lots of debug build logs are available in verbose in GUI rather than just a `.log` file.
2. Or open the log file and search for `error` or `errors generated.` or `error generated.` in your log file. This will give you which file is failing on CLI.

Usually it happens due to multiple different Xcode versions on GUI and `xcode-select` path set for CLI.
So it comes down to a making sure that whatever tool you're using is on same versions either GUI or CLI. And sometimes `hotfixes` or `build-fixes` are merged in latest `develop` , `main` or `tag` so make sure the branch you're working on is also updated with latest merges from parent branches or protected branches.

Or else you can face a classic `It Works on my machine!` or `Multiple Spiderman pointing at each other` meme IRL.



## Console Debug

When you have specified the breakpoint and you have lldb debugger in the console.

You could use it

```llvm
po swift\_variable/ objects
```

[SO link](https://stackoverflow.com/questions/4735156/xcode-debugger-view-value-of-variable) [Apple Doc](https://developer.apple.com/library/archive/documentation/DeveloperTools/Conceptual/debugging_with_xcode/chapters/debugging_tools.html) [Complete Guide](https://andela.com/insights/the-complete-guide-to-debug-swift-code-with-lldb/) [LLDB Debug](https://medium.com/flawless-app-stories/debugging-swift-code-with-lldb-b30c5cf2fd49) [Advanced LLDB](https://medium.com/@fadiderias/xcode-and-lldb-advanced-debugging-tutorial-part-1-31919aa149e0)

## [Breakpoint](breakpoint.md)

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



## Assign variables in runtime

```llvm
e let $data = CustomObject()
po $data
```

print a more readable Dictionary object via lldb
```llvm
po print(dictionaryType)
```
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



## Crash

[apple dev | Diagnosing issues using crash reports and device logs](https://developer.apple.com/documentation/xcode/diagnosing-issues-using-crash-reports-and-device-logs)

## Method_Swizzling

You can reverse engineer certain libraries / frameworks of apple UIKit , AppKit and utilize objective-C runtime methods to quickly replace our own implementation of the method we want to override.
Sometimes the library we are consuming won't expose all the options to tweak or change its behavior so method swizzling basically comes into the picture where you just hack / capture the memory and replace it with our own custom function / method. To get more custom behavior and just understand the underlying working architecture of the abstracted library.

Haven't heard anyone explicit mention this most of the time but one senior engineer from Objective - C did gave me a nudge to check it out in 2020 just because I mentioned I came from Turbo-C , DosBox and C++ compilers era.

## access hidden func inits

Utilizing Objective-C runtime classes to have a work around since some APIs don't allow to subclass things to create test mocks

```swift
static func loader() -> MockAssetResourceLoader { 
	let allocated = MockAssetResourceLoader
		.perform(NSSelectorFromString("alloc")) 
	return allocated?
		.takeRetainedValue() as! MockAssetResourceLoader 
}
```

## Custom Debug String

Enforcing a struct with protocol `CustomDebugStringConvertible` and use `debugDescription` computed property to provide more information for getting customized console prints.

### Definition

```swift
struct TrackCodecs: CustomDebugStringConvertible {
    var audioCodec: [String]
    var textCodec: [String]
    var closedCaptionCodec: [String]
    var subtitleCodec: [String]
    
    var debugDescription: String {
        """
          Current Media Asset Info
          Type: Audio | Codec: \(audioCodec)
          Type: Text | Codec: \(textCodec)
          Type: Audio | Codec: \(closedCaptionCodec)
          Type: Subtitle | Codec: \(subtitleCodec)
          ------------------------
        """
    }
}
```

### Usage

```swift
let codec = TrackCodecs(...)
print(codec.debugDescription)
```

Read more by [Avanderlee | article](https://www.avanderlee.com/swift/custom-debug-descriptions/)


## Convert data to String

Could be helpful for converting String data into String object with its default encoding provider.

```swift
if let accessLog: AVPlayerItemAccessLog = playerItem?.accessLog(),
   let errorLog: AVPlayerItemErrorLog = playerItem?.errorLog() {
	print("$$$ avFoundationFailure")
	if let dataError = errorLog.extendedLogData() {
		let convertedString = NSString(data: dataError, encoding: errorLog.extendedLogDataStringEncoding)
		
		print("ASCII string: \(convertedString ?? "Conversion failed.")")
		print(" ------------ ")
		print(accessLog)
	}
}
```

[the-ultimate-guide-to-converting-swift-data-to-string](https://www.dhiwise.com/post/the-ultimate-guide-to-converting-swift-data-to-string)


## Framework swapping

[Debugging framework post](/ios/library/framework#Debugging)

[SO | how-to-debug-framework-source-from-main-project](https://stackoverflow.com/questions/13836628/how-to-debug-framework-source-from-main-project)

[SO | post debugger not showing variable names objc](https://stackoverflow.com/questions/31219422/swift-debugger-does-not-show-variable-values-when-importing-objc-framework)

[SO | swift-debugger-does-not-show-variable-values-when-importing-objc-framework](https://stackoverflow.com/questions/31219422/swift-debugger-does-not-show-variable-values-when-importing-objc-framework)



There is actually a way to debug the an iOS project that uses a .framework, if you have the source code. This worked for me in xcode 4.6.

You can do in the following way:

1. Insert breakpoints in your .framework's source code.
2. Compile the project that uses the framework and run it on your device (iPhone, iPad, etc.). This step is just to make sure you have the most updated project installed on your device.
3. Stop the process running on your device and go to xcode -> product -> Attach to process -> _YourApp_. In xcode 6, "Attach to Process" is under the Debug menu.

If you don't see your app's name in the applications listed there, go to "By process Identifier (PID) or Name..." and enter the app's name. Now, if you'll run the application in your device, it should break in the breakpoints that are enabled.

[SO source](https://stackoverflow.com/a/16812890)

## Debug Release App

Normally Debug builds have optimisation disabled (`-O0`) to make debugging easier, whereas Release builds have optimisation enabled (`-O3` or `-Os`), which makes the code run much faster, but also makes debugging harder (but not impossible). You can just go into the build settings in Xcode in the Debug configuration and temporarily turn up the optimisation level - this will keep all the other debug goodies (symbols etc) but hopefully also flush out the Release mode bug. (Don't forget to reset the optimisation level to `-O0` in the Debug configuration when you're done!)

Run code in release or not


```swift
#if DEBUG
    print("Debug")
#else
    print("Release")
#endif
```
[sarunw | Run code in Release build](https://sarunw.com/posts/run-code-in-release-build-in-xcode/)

[sarunw | check-if-swift-code-is-in-debug-build-configuration](https://sarunw.com/posts/how-to-check-if-swift-code-is-in-debug-build-configuration/)

## Search Cryptic Errors

[apple developer forums](https://developer.apple.com/forums/) could be the best resource when searching for cryptic error messages which aren't documented or verbose enough for the console logs.

Usually people on the forum respond towards it, rather than Stack overflow.
