# Test

## Test Pattern

## Unit Test

Every unit test follows this general pattern:  

1.  setup some object under test
2.  provide the object under test some input
3.  make assertions on the objects outputs

## Skip Tests

You can append `skip` to the test_function_name in order for Xcode compiler | runtime service to skip those tests in order to be ran and not wasted with that resources accordingly.

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

[SO | skip-multi-tests-in-xcode](https://stackoverflow.com/questions/64025146/skip-multi-tests-in-xcode)

[skipping-tests-in-xcode](https://www.matrixprojects.net/p/skipping-tests-in-xcode/)

## setUp

```swift
class PPVSSLoaderDelegateTests: XCTestCase {
	var mockVSSDelegate: MockVSSDelegate!

	override func setUp()  {
      mockVSSDelegate = MockVSSDelegate()
    }
}
```

## Teardown

```swift
class PPVSSLoaderDelegateTests: XCTestCase {
	var mockVSSDelegate: MockVSSDelegate!

	override func tearDown()  {
      mockVSSDelegate.reset()
    }
}
```
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

## Testable

In order to access internal classes to our unit / ui test target, we can utilize the following keyword `testable` in order to gain elevated access to its internal implementation.

```swift
@testable import MainAppModuleName
```

Note: 
- We still can't access private functions or variables with this.
- You can resort to `private(set)` for the properties to make tests which can be just read for unit testing.

[how-to-unit-test-private-methods-in-swift](https://cocoacasts.com/how-to-unit-test-private-methods-in-swift)

## Assertions

– `assert()`  
– `precondition()`  
– `assertionFailure()`  
– `preconditionFailure()`  
– `fatalError()`


```swift
assert(10 > 5, "10 is not less than 5")
```

[swift assertions](https://andybargh.com/swift-assertions/)

[Swift by sundell | picking-the-right-way-of-failing-in-swift](https://www.swiftbysundell.com/articles/picking-the-right-way-of-failing-in-swift/)

## Simulators vs emulators

[testing-on-real-devices-vs-simulators-vs-emulators](https://www.testingxperts.com/blog/testing-on-real-devices-vs-simulators-vs-emulators/ca-en)

## CI / CD

[fastlane | run tests](https://docs.fastlane.tools/actions/run_tests/)

[speed-up-ios-ci-using-test-without-building-xctestrun-and-fastlane](https://medium.com/xcblog/speed-up-ios-ci-using-test-without-building-xctestrun-and-fastlane-a982b0060676)

## Links

[wwdc 20 notes](https://www.wwdcnotes.com/notes/wwdc20/10164/)

[apple dev | xcTest](https://developer.apple.com/documentation/xctest/3521325-xctskipif)

[apple dev | xcTest setup with error](https://developer.apple.com/documentation/xctest/xctest/3521150-setupwitherror)

[xctest-setup-and-teardown-are-not-dead-yet](https://hackernoon.com/swift-xctest-setup-and-teardown-are-not-dead-yet)

## Tools

[setup-xcode-and-appium-for-ios-automation-real-device](https://blog.emumba.com/setup-xcode-and-appium-for-ios-automation-real-device-6d6d86874ae1)

[ios-testing-tools](https://www.lambdatest.com/blog/ios-testing-tools/)

[top-5-ios-testing-frameworks](https://saucelabs.com/resources/blog/top-5-ios-testing-frameworks)

[automated testing solutions](https://www.mobot.io/blog/the-8-best-ios-automated-testing-solutions-in-2022)

[ios-test-automation-challenges-and-solutions](https://sofy.ai/blog/ios-test-automation-challenges-and-solutions/)
