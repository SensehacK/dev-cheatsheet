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


## Compare Error


```swift
public func == (lhs: Error, rhs: Error) -> Bool {
    guard type(of: lhs) == type(of: rhs) else { return false }
    let error1 = lhs as NSError
    let error2 = rhs as NSError
    return error1.domain == error2.domain && error1.code == error2.code && "\(lhs)" == "\(rhs)"
}

extension Equatable where Self : Error {
    public static func == (lhs: Self, rhs: Self) -> Bool {
        lhs as Error == rhs as Error
    }
}
```



https://stackoverflow.com/questions/49658919/is-there-a-better-way-to-compare-errors-in-swift