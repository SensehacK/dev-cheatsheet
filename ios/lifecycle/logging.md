
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

