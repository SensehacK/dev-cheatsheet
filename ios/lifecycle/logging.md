

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

