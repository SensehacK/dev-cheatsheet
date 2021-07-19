# Error state

## State



## Stringify Extension

We can extend error localized description types to string extension for appending different objects and formatting it appropriately.

```swift 
extension String {
    
    public func addingErrorInfo(context: ErrorObj) -> String {
        let errorInfo = ErrorInfo(error: context)
        return "\(self)\(Symbols.newline)\(errorInfo.systemVersion), \(errorInfo.modelName), \(errorInfo.connectivityState), \(errorInfo.appVersion)."
    }
    
    public func addingRetryErrorInfo() -> String {
        return
            " \(self)\(Symbols.newline)\(Symbols.newline) \(Strings.Functionality.retryDescription)"
    }
    
}


public struct Symbols {
		public static let at = "@"
		public static let newline = "\n"
}

```