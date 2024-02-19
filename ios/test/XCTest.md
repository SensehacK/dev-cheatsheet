# XCTest


Testing on Real Devices

[testing-on-real-devices-vs-simulators-vs-emulators](https://www.testingxperts.com/blog/testing-on-real-devices-vs-simulators-vs-emulators/ca-en)


## Expectation

[apple dev | expectations](https://developer.apple.com/documentation/xctest/asynchronous_tests_and_expectations)

[HWS | asynchronous-functions-using-expectation](https://www.hackingwithswift.com/example-code/testing/how-to-test-asynchronous-functions-using-expectation)

[medium | 4-tips-to-master-xctestexpectation](https://medium.com/blablacar/4-tips-to-master-xctestexpectation-aee2b2631d93)

## Multiple Expectations 

If the error is 
`API violation - multiple calls made (NSInternalInconsistencyException)`

You could use another function for wait in XCTest which takes an array of expectations.

```swift
func test_whenTwoThingsAreDone_thenDoSuccessChecks() {
	let firstExpectation = self.expectation(description: "First expectation fulfilled")
	let secondExpectation = self.expectation(description: "Second expectation fulfilled")

	doSomething { data, error in 
		// Check for data
		XCTAssertNotNil(data)
		firstExpectation.fulfill()
	}

	doSomething2 { data, error in 
		// Check for data
		XCTAssertNotNil(data)
		secondExpectation.fulfill()
	}
	
	wait(for: [firstExpectation, secondExpectation], timeout: 0.5)
}
```

`wait(for: [exp1, exp2], timeout: 0.5)` is easier to deal with when having multiple async checks overall.

[apple dev | wait for expectations](https://developer.apple.com/documentation/xctest/xctestcase/1500748-waitforexpectations)



## Unwrap Throws

Mark the function as `throws` and unwrap optional values to non optional so that you can work with it.

```swift
func test_URL() throws {
	let url = URL(string: "https://sensehack.github.io/")
	// URL is of type URL?
	let unwrapURL = try XCTUnwrap(url)					
}
```

## OR conditions 

You can have two conditions check as well in XCTAssert


```swift
XCTAssert(result.isEqual(expected1) || result.isEqual(expected2))
```

Test Assertions

[swift by sundell | test-assertions-in-swift](https://www.swiftbysundell.com/articles/test-assertions-in-swift/)

## Resources

[nshipster | xctestcase](https://nshipster.com/xctestcase/)

[the-ultimate-guide-to-unit-and-ui-testing-for-beginners-in-swift](https://www.bitrise.io/blog/post/the-ultimate-guide-to-unit-and-ui-testing-for-beginners-in-swift)


[how-to-write-automated-tests-for-ios](https://www.toptal.com/ios/how-to-write-automated-tests-for-ios)
