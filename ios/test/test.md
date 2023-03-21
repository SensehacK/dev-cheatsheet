# Test


## Test Pattern

## Unit Test

Every unit test follows this general pattern:  

1.  setup some object under test
2.  provide the object under test some input
3.  make assertions on the objects outputs




## Skip Tests

You can append `skip` to the test_function_name in order for Xcode compiler | runtime service to skip those tests in order to be ranned and not wasted with that resources accordingly.

Really handy when you're working with `flaky` tests


## Conditional Skip Testing

You could utilize the various ways to skip testing if certain conditions have been met.

```swift
guard let envValue = ProcessInfo.processInfo.environment["IS_CI_SERVER"] else { return }
try XCTSkipIf(envValue == "true")
```

You could embed this code in Test life cycle methods which is present for setting up code / environment before running the main test case.

- func setUp() { }
- func setUpWithError() throws { }

The `setUpWithError` is the right candidate for skipping tests without adding that skip_logic for every unit tests. You can just include that information in the Test_Class file.
Clean and less verbose.


## Warnings

`Errors thrown from here are not handled` - this appears when you're trying to call a function which can throw an error. Swift needs to either do a `try catch` to handle the thrown error or mark the test function with `throws`

```swift

func test_whenSomething_ThenBehavior() throws {
	let unwrappedDate = try callUnwrappingFunction() // Warning
}
```


## Unwrapping while Testing

We should be careful to use force unwrapping when handling optionals in tests. if for some reason it's `nil` the tests are going to crash. that's not a super big deal when running locally but if that happens when running in CI it's going to force a restart of the tests and not give us much to go on as to why the crash occurred. better to treat this case as a test failure rather than crashing so that the tests report the failure and then continue - `Test guru - mentor`

```swift
func test_objectCreation_UsingJSONMapping() {
	let object: ObjectType = getMappedObject(for: TestJSON.Object)!
}
```

Solution

```swift
func test_objectCreation_UsingJSONMapping() throws {
	let object: ObjectType = try XCTUnwrap(getMappedObject(for: TestJSON.Object))
}
```


## Extension

Simple wrapper functions to make assertions a bit more readable at call sites and so we don't have to constantly prefix assertions with `XCT`.

```swift
public struct Assert<TestValueType> {
    private let testValue: TestValueType
    public init(_ testValue: TestValueType) {
        self.testValue = testValue
    }
}
```

```swift
// MARK: - Identity

extension Assert where TestValueType == Optional<AnyObject> {

    public func isIdentical<R>(to expression: @autoclosure () throws -> R, message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) where R == TestValueType {
        XCTAssertIdentical(testValue, try expression(), message(),  file: file, line: line)
    }

    public func isNotIdentical<R>(to expression: @autoclosure () throws -> R, message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) where R == TestValueType {
        XCTAssertNotIdentical(testValue, try expression(), message(),  file: file, line: line)
    }

}
```

```swift
// MARK: - Optional

extension Assert where TestValueType == Optional<Any> {

    public func isNil(message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertNil(testValue, message(),  file: file, line: line)
    }

    public func isNotNil(message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertNotNil(testValue, message(),  file: file, line: line)
    }

}
```

```swift

// MARK: - Equatable
extension Assert where TestValueType: Equatable {

    public func isEqual(to expression: @autoclosure () throws -> TestValueType, message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertEqual(testValue, try expression(), message(), file: file, line: line)
    }

    public func isNotEqual(to expression: @autoclosure () throws -> TestValueType, message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertNotEqual(testValue, try expression(), message(), file: file, line: line)
    }

}
```

```swift
// MARK: - Floating Point
extension Assert where TestValueType: FloatingPoint {

    public func isEqual(to expression: @autoclosure () throws -> TestValueType, withAccuracy accuracy: TestValueType, message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertEqual(testValue, try expression(), accuracy: accuracy, message(), file: file, line: line)
    }

    public func isNotEqual(to expression: @autoclosure () throws -> TestValueType, withAccuracy accuracy: TestValueType, message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertNotEqual(testValue, try expression(), accuracy: accuracy, message(), file: file, line: line)
    }

}
```

  
```swift
// MARK: - Numeric
extension Assert where TestValueType: Numeric {

    public func isEqual(to expression1: @autoclosure () throws -> TestValueType, withAccuracy accuracy: TestValueType, message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertEqual(testValue, try expression1(), accuracy: accuracy, message(), file: file, line: line)
    }

    public func isNotEqual(to expression1: @autoclosure () throws -> TestValueType, withAccuracy accuracy: TestValueType, message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertNotEqual(testValue, try expression1(), accuracy: accuracy, message(), file: file, line: line)
    }
}
```

```swift
// MARK: - Boolean

extension Assert where TestValueType == Optional<Bool> {

    public func isFalse(message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertFalse(testValue ?? true, message(), file: file, line: line)
    }

    public func isTrue(message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertTrue(testValue ?? false, message(), file: file, line: line)
    }

}
```

```swift
// MARK: - Comparable

extension Assert where TestValueType: Comparable {

    public func isGreaterThan(_ expression: @autoclosure () throws -> TestValueType, _ message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertGreaterThan(testValue, try expression(), message(),  file: file, line: line)
    }

    public func isGreaterThanOrEqual(to expression: @autoclosure () throws -> TestValueType, message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertGreaterThanOrEqual(testValue, try expression(), message(),  file: file, line: line)
    }

    public func isLessThan(_ expression: @autoclosure () throws -> TestValueType, _ message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertLessThan(testValue, try expression(), message(),  file: file, line: line)
    }

  

    public func isLessThanOrEqual(to expression: @autoclosure () throws -> TestValueType, message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertLessThanOrEqual(testValue, try expression(), message(),  file: file, line: line)
    }

}

```

```swift
// MARK: - Throwing

extension Assert {
    public struct Function<ReturnType> {
        private let testExpression: () throws -> ReturnType
        init(_ testExpression: @autoclosure @escaping () throws -> ReturnType) {
            self.testExpression = testExpression
        }
    }
}

extension Assert.Function {
    public func doesNotThrow(message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertNoThrow(testExpression, message(), file: file, line: line)
    }

    public func throwsError(errorHandler: (_ error: Error) -> Void = { _ in }, message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTAssertThrowsError(testExpression, message(), file: file, line: line, errorHandler)
    }
}

public func Unwrap<T>(_ expression: @autoclosure () throws -> T?, _ message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) throws -> T {
    return try XCTUnwrap(expression())
}
```
## Links

https://stackoverflow.com/questions/64025146/skip-multi-tests-in-xcode

https://www.wwdcnotes.com/notes/wwdc20/10164/

https://developer.apple.com/documentation/xctest/3521325-xctskipif

https://developer.apple.com/documentation/xctest/xctest/3521150-setupwitherror

https://docs.fastlane.tools/actions/run_tests/

https://www.matrixprojects.net/p/skipping-tests-in-xcode/

https://medium.com/xcblog/speed-up-ios-ci-using-test-without-building-xctestrun-and-fastlane-a982b0060676