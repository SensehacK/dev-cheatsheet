
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


## References

https://www.swiftbysundell.com/articles/unit-testing-asynchronous-swift-code/#expectations

https://www.swiftbysundell.com/articles/unit-testing-code-that-uses-async-await/

Refactoring code for testability
https://www.swiftbysundell.com/articles/refactoring-swift-code-for-testability/