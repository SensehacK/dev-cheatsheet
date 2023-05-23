# Test Extension


Simple wrapper functions to make assertions a bit more readable at call sites and so we don't have to constantly prefix assertions with `XCT`.

## Assert

```swift
public struct Assert<TestValueType> {
    private let testValue: TestValueType
    public init(_ testValue: TestValueType) {
        self.testValue = testValue
    }
}
```

## Identity

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

## Optional

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

## Equatable

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

## Floating Point
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

## Numeric

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

## Boolean

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

## Comparable

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

## Throwing

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