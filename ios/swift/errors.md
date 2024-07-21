

## Implementation

### Enum based

The simplest approach is probably to define _one_ custom `enum` with just one `case` that has a `String` attached to it:

```swift
enum MyError: Error {
    case runtimeError(String)
}

extension MyError: LocalizedError {
	var errorDescription: String? {
        switch self {
	    case .runtimeError(let str):
		    "RunTime Error: \(str)"
        }
    }
}
```

Example usage would be something like:

```swift
func someFunction() throws {
    throw MyError.runtimeError("some message")
}
do {
    try someFunction()
} catch MyError.runtimeError(let errorMessage) {
    print(errorMessage)
}
```

If you wish to use existing `Error` types, the most general one would be an `NSError`, and you could make a factory method to create and throw one with a custom message.


### Struct based

Or use another approach 

```swift
struct RuntimeError: LocalizedError {
    let description: String

    init(_ description: String) {
        self.description = description
    }

    var errorDescription: String? {
        description
    }
}
```



And to use:

```swift
throw RuntimeError("Error message.")
```

[SO | reference code snippets](https://stackoverflow.com/questions/31443645/simplest-way-to-throw-an-error-exception-with-a-custom-message-in-swift)

## Mind Map

[check errors in testing](check_error.md)



## Error Handling


[syntax try catch](https://www.hackingwithswift.com/new-syntax-swift-2-error-handling-try-catch)

[try catch handling](https://www.avanderlee.com/swift/try-catch-throw-error-handling/)

[SO | generate-your-own-error-code-in-swift](https://stackoverflow.com/questions/40671991/generate-your-own-error-code-in-swift-3)

