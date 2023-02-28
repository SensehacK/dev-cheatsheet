

Testing on Real Devices

https://www.testingxperts.com/blog/testing-on-real-devices-vs-simulators-vs-emulators/ca-en


## Expectation

https://developer.apple.com/documentation/xctest/asynchronous_tests_and_expectations

https://www.hackingwithswift.com/example-code/testing/how-to-test-asynchronous-functions-using-expectation

https://medium.com/blablacar/4-tips-to-master-xctestexpectation-aee2b2631d93


## Unwrap Throws

Mark the function as `throws` and unwrap optional values to non optional so that you can work with it.

```swift
func test_URL() throws {
	let url = URL(string: "https://sensehack.github.io/")
	// URL is of type URL?
	let unwrapURL = try XCTUnwrap(url)					
}
```



Test Assertions

https://www.swiftbysundell.com/articles/test-assertions-in-swift/

## Resources

https://nshipster.com/xctestcase/

https://www.bitrise.io/blog/post/the-ultimate-guide-to-unit-and-ui-testing-for-beginners-in-swift


https://www.toptal.com/ios/how-to-write-automated-tests-for-ios