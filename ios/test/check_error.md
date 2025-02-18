# Check Error


```swift 

XCTAssertThrowsError

XCTAssert(error)
```


```swift
class Translator {
    func translate(_ text: String) throws -> String {
        ...
    }
}


// Usage

func testFunc() {
		// Capture the thrown error using a closure
	XCTAssertThrowsError(try translator.translate("")) {
		thrownError = $0
	}

	// First we’ll verify that the error is of the right
	// type, to make debugging easier in case of failures.
	XCTAssertTrue(
		thrownError is Translator.Error,
		"Unexpected error type: \(type(of: thrownError))"
	)

	// Verify that our error is equal to what we expect
	XCTAssertEqual(thrownError as? Translator.Error, .emptyText)
}
```


[Testing error code path in swift | swift by sundell](https://www.swiftbysundell.com/articles/testing-error-code-paths-in-swift/)

## Mind Map

[errors](/ios/swift/errors.md)