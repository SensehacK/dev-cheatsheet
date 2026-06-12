

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


## References

[apple dev | errors and exceptions](https://developer.apple.com/documentation/foundation/errors-and-exceptions)

[apple archive | error handling guide](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/ErrorHandlingCocoa/ErrorHandling/ErrorHandling.html#//apple_ref/doc/uid/TP40001806)



## NS Error

Information about an error condition including a domain, a domain-specific error code, and application-specific information.

## Exception


> Use [`NSException`](https://developer.apple.com/documentation/foundation/nsexception) to implement exception handling. An exception is a special condition that interrupts the normal flow of program execution. Each application can interrupt the program for different reasons. For example, one application might interpret saving a file in a directory that is write-protected as an exception. In this sense, the exception is equivalent to an error. Another application might interpret the user’s key-press (for example, Control-C) as an exception: an indication that a long-running process should abort.

[apple docs](https://developer.apple.com/documentation/foundation/nsexception)


## Munging

Swift error "munging" (mapping, wrapping, or converting) involves transforming low-level errors into domain-specific, user-friendly, or actionable errors using the

`Error` protocol, `enum`s with associated values, and `do-catch` blocks. It improves code readability, enhances debugging, and provides better user experience by separating raw failures from presented messages.


### Threads

> We never care for this extra duplicate error passed in the Events.Warning(EngineError) interface, since we also embed the same thing in EngineData.error.

The idea was to send the Event with `event.underlyingError == engineData.error` . The former is meant to be used when you want to quickly access the error without caring about `EngineData`. IIRC, we added `EngineData` later on to account for more properties to avoid bloating the Event.

> Since we already do assign underlyingError prop in zephyr, why do we have to extract or cast it to NSError to get more underlying info?

`NSError` is going to have more properties that help you determine a specific failure reason, mainly `domain` and `code` and sometimes `userInfo` is useful too. `Domain` and `code` help you pinpoint specific things like `domain == CoreMediaErrorDomain` and `code == -12938` would translate to HTTP 404 not found.

If you only have `Error` you would have to know the specific type in advance to cast it to something useful and that's not always possible.

> Is CustomNSError -> NSError in hindsight same thing when casting, I'm leaning towards yes here.

In Swift you can always cast `Swift.Error as NSError` with no penalty - it always succeeds. What happens is Swift will try to fill out the `domain` and `code` properties as best it can from the `Swift.Error`. A process they call "munging" - sometimes it doesn't always get it right and you'll often see `code` default to something like `0` and the `domain` is maybe the name of the `type` of `Error`

`CustomNSError` makes this cast more accurate. If your error type conforms to it, casting to `NSError` will always yield the expected properties.