
# Asynchronous Tests

Testing normal synchronous code is pretty easy to begin with Swift. Usually the next step of writing better code is testing asynchronous code which returns values after indeterminate amount of time.


## Use case

Most of the iOS code you would work on is asynchronous in nature. 
Making any network request, using DispatchQueues or any Concurrency related library to make concurrent task execution.
Testing non definitive behavior is crucial for making sure we aren't missing any edge case scenarios.

eg. 
Your app gets input entered and then that input is sent over to a network service to get some results. Depending on lot of external factors that network service will get us a response of failure or success with some data in x amount of time. 

Our scheduler or main thread or CPU processor won't waste its time waiting for its response to come back. So it will context switch and move on to next thing. But it will keep its thread or process open to observing the original network request you made. Once the network request comes back with some value, the cpu will context switch and return us the result back.

We would want to test this `x` amount of time it takes for something to happen or does it fail or succeeds. It is indeterministic in nature.



## Enter Expectations

With Expectations in Xcode testing framework, we can define certain expectations in the beginning of the asynchronous task. The  XC framework expectation will wait for some amount of time and then if the appropriate data is passed / returned we can manually set the expectations to be fulfilled or failed.

We can have multiple expectations in our test function.

Define an expectation
```swift
let expectation = self.expectation(description: "Your custom expectation")
```


## Code

Basic unit test  `Expectation` working with Asynchronous closure based task.

```swift
func test_something_async() {
	var resultData: [Model]?
	var expectedResultData: [Model] = [333, 666, 999]
	let expectation = self.expectation()

	doSomeAsyncTask { result in 
		if result == success {
			resultData = result
			expectation.fulfill()
		}
	}

	waitForExpectations(timeout: 2, handler: nil)
	XCTAssertEqual(resultData?.count, 
	expectedResultData.count)
}
```

Or moving forward you can utilize 

```swift
await fulfillment(of: [expectation], timeout: 2)
```

## Caveat  Async Await

Async Await makes writing asynchronous tests a bit simpler. 
Because now we can do synchronous ways of certain asynchronous tasks. It helps us to read through like the normal synchronous way of execution.


## Explicit Wait

You can use [XCTWaiter.wait](https://developer.apple.com/documentation/xctest/xctwaiter) functions.

For example:

```swift
let exp = expectation(description: "Test after 5 seconds")
let result = XCTWaiter.wait(for: [exp], timeout: 5.0)
if result == XCTWaiter.Result.timedOut {
    XCTAssert(<test if state is correct after this delay>)
} else {
    XCTFail("Delay interrupted")
}
```


## DispatchQueue Wait + Expectation

You can combine DispatchQueue async wait and use expectations for swift unit tests to wait for some time in order to get the results needed for testing.

```swift
func testWhen() {
	let expectation = self.expectation(description: "TextTracksPresent")
expectation.expectedFulfillmentCount = 1

DispatchQueue.main.asyncAfter(deadline: .now()+3 ) {
		print("Check after 3 secs??")
		XCTAssertEqual(self.currentTrack.id, audioTrack.id)
		expectation.fulfill()
	}
waitForExpectations(timeout: 5)
}

```
## References

[swift by sundell | unit-testing-asynchronous-swift-code Expectations](https://www.swiftbysundell.com/articles/unit-testing-asynchronous-swift-code/#expectations)

[swift by sundell | unit-testing-code-that-uses-async-await](https://www.swiftbysundell.com/articles/unit-testing-code-that-uses-async-await/)

[swift by sundell | Refactoring code for testability](https://www.swiftbysundell.com/articles/refactoring-swift-code-for-testability/)

[SO | how-to-wait-in-a-xctest](https://stackoverflow.com/questions/50247929/how-to-wait-in-a-xctest-for-t-seconds-without-timeout-error)
