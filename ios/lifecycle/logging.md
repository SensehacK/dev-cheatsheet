
## Unified Logging

Apple recently introduced `os_log` and unified logging mechanism for iOS 14/15 which made it easier for developer to work with logging solution by apple.



## Log levels

```swift

/// The levels of logs we support.
public enum LogLevel: String {
    /// Verbose
    case v = "🔘"

    /// Debug
    case d = "🟡"

    /// Info
    case i = "ℹ️"

    /// Warning
    case w = "⚠️" 

    /// Error
    case e = "‼️"

    /// Fatal
    case f = "🔥"

    var priority: Int {
        switch self {
        case .v: return 0
        case .d: return 1
        case .i: return 2
        case .w: return 3
        case .e: return 4
        case .f: return 5
        }
    }
}

```


## Console log prefix filtering

Having a prefix to your debugging logs when working on a big feature or bug hunt is crucial as well.

```swift
print("CUSTOM_FLAG: ")
print("$$$ \(someVariable)")
```
In Xcode -> console log GUI. At the right most bottom corner you can specify your string `prefix` and only get filtered logs for easier confirmation of code path execution being carried out.

Helps me sift through bunch of non related console / debug prints from large projects where if you don't want to mess around with disabling those analytics flags or configs to not print out junk logs in the console at the given moment.

This is if your project has non structured logging API, if you have appropriate subsystems designated for `Unified Logging API` with Xcode 15+ you get more advance filters to work around your problem. 


## Stop using Print

```swift
func print(_ items: Any..., separator: String = ", ", terminator: String = "\n") {
    preconditionFailure("STOP using print()")
}
```


## HotSwap print to osLog

Update the framework or library if using SPM to enable debug flag

```swift
swiftSettings: [.define("DEBUG",
				.when(configuration: .debug))]
```

Change the old global print or debugPrint code

```swift
import OSLog
@available(iOS 14.0, *)
public extension Logger {
    /// Using your bundle identifier is a great way to ensure a unique identifier.
    private static var subsystem = Bundle.main.bundleIdentifier!

    /// All logs related to Client Events.
    static let customLogger = Logger(subsystem: subsystem, category: "CustomProj")
}


func projDebugPrint(_ string: String, withLogOption logOption: ProjDebugOptions, withDebugOptions debugOptions: ProjDebugOptions) {
    // Disable this check or make sure we provide the right debug options.
    if debugOptions.contains(logOption) {
        if #available(iOS 14.0, *) {
            Logger.customLogger.debug("$$$$$ Kay\(_getPrefix()) \(string)")
        } else {
            // Fallback on earlier versions
            NSLog("@@@@@ Kay \(_getPrefix()) \(string)")
            print("\(_getPrefix()) \(string)")
        }
    }
}
```


PS. You may have to download a profile in order to enable private logs from here -> [show-private-logs-in-macos-catalina](https://georgegarside.com/blog/macos/sierra-console-private/#show-private-logs-in-macos-catalina-10153)

Debug prints not appearing in os console app? 
You may have to enable them from Menu Bar -> Action -> Include Debug messages


## CLI

Use command `log` to quickly generate logs or capture them from connected device.

```sh
sudo log collect --device --start "2020-06-25 16:10:00" --output myapp.logarchive
```


## Limit 1024 Chars

Truncate os_log

[SO | post about os_log](https://stackoverflow.com/a/40283623)

Split string extension to overcome this os limitation.
[SO | string extension](https://stackoverflow.com/a/76776120)

## References

[swift dev | logging for beginners](https://theswiftdev.com/logging-for-beginners-in-swift/)

[Filtering logs in OS Console app](https://support.apple.com/lv-lv/guide/console/cnslbf30b61a/mac)
