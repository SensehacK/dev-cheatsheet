# RxTest

I thought I would write down my RxTest / RxSwift Unit testing / XCTests journey in this file. Since I already have a folder dedicated towards testing in iOS folder.



## Sequence Matters

So I don't know if this is the matter of Hot / Cold observables but if it is I have to pin point you to the hot / cold observables playground in RxLearning repo or Swift Playgrounds Repo.

I spent around 1 hour debugging this to why my XCTest `expectations` were failing when I was trying to achieve similar level of unit tests 


Failing Code

```swift
func test_NoLoggedInUser_BeforeUserSignUpActionIsPerformed() throws {
	// Open up Signup action
	testObject.input.signUpAction.onNext(())  // Diff
	
	let expectation = self.expectation(description: "Sign Up Button Pressed - Results in View Presentation")

	// Observe the ViewModel Output
	testObject
		.output
		.navigationContext
		.asObservable()
		.subscribe(onNext: { context in
			Assert(context).isNotNil()
			expectation.fulfill()
		})
		.disposed(by: disposeBag)
		
	waitForExpectations(timeout: 1)
}
```

Working Code

```swift
func test_NoLoggedInUser_BeforeUserSignUpActionIsPerformed() throws {
	let expectation = self.expectation(description: "Sign Up Button Pressed - Results in View Presentation")

	// Observe the ViewModel Output
	testObject
		.output
		.navigationContext
		.asObservable()
		.subscribe(onNext: { context in
			Assert(context).isNotNil()
			expectation.fulfill()
		})
		.disposed(by: disposeBag)

	// Open up Signup action
	testObject.input.signUpAction.onNext(())  // Diff
	waitForExpectations(timeout: 1)
}
```

Noticed the only difference is the structure of events being sent out. 
Imposter Syndrome ??
Now this maybe a novice mistake but I'm dumb enough to make it and I wanted this to be documented in order for future me or whoever stumbled upon this piece of code block in Rx world to know that you aren't the only one who makes these kinds of mistakes.
I have 5 years of Software Engineer Development Experience and maybe 6 - 9 months of Reactive Paradigm experience using RxSwift.  Of course I never wrote lot of tests and this was my first hand experienced taking a crack at RxSwift codebase unit testing.

### Note
This reorganizing of lines works because (& this is my assumption) that the output needs to be subscribed first and when we first send the input `signUpAction` next event. The next code block hasn't yet being subscribed to listened to its events. Maybe a Cold observable at this instance or just no observable. But I'm spitballing over here.

Even `waitForExpectations(timeout: 1)` should be after the `Event.onNext(_)` fires its respective event or input or else the test case fails.



## RxChain Paths

Determining how RxChain paths work with every failable condition. Those unique paths should be mapped down as unit tests.

Example Rx Chain Code

```swift
// Parse authentication
let (auth, nilAuth) = successBody
	.map { body -> Authentication? in
		guard let response = body as? String else {
			return nil
		}
		return Authentication(JSONString: response)
	}
	.share()
	.split()
```

Rx Tests of 3 different unit tests

```swift
func test_whenSuccessEventIsReceived_And_ResponseBodyIsNotAString_thenErrorViewStateIsEmitted() { }

func test_whenSuccessEventIsReceived_And_ResponseBodyIsANotAnAuthenticationObject_thenErrorViewStateIsEmitted() { }

func test_whenSuccessEventIsReceived_And_ResponseBodyIsAnAuthenticationObject_thenSessionCoordinatorEntryRequestIsEmitted() { }

```



```swift
// MARK: - RxTest Helpers

public struct Fail {
    @discardableResult
    public init(message: String = "", file: StaticString = #filePath, line: UInt = #line) {
        XCTFail(message, file: file, line: line)
    }
}

public struct Assert<TestValueType> {
    private let testValue: TestValueType
    public init(_ testValue: TestValueType) {
        self.testValue = testValue
    }
}

public extension Assert {

    func isEqual<T>(to expression: @autoclosure () throws -> [T], message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) where TestValueType == [Recorded<Event<T>>], T: Equatable {
        guard let comparator = try? expression() else {
            Fail(message: message(), file: file, line: line)
            return
        }
        XCTAssertRecordedElements(testValue, comparator, file: file, line: line)
    }
    
}
```

## Scheduler 

Timing tests
https://kean.blog/post/rxswift-testing

TestScheduler - RxSwift
https://www.youtube.com/watch?v=HKigVK1eqwE

## Unit tests

https://betterprogramming.pub/rxswift-unit-testing-explained-in-3-minutes-c024b7a26d

https://www.kodeco.com/7408-testing-your-rxswift-code

https://fivenyc.medium.com/testing-rxswift-code-how-i-learned-to-stop-worrying-and-love-writing-unit-tests-part-2-a39b61906e55

https://www.youtube.com/watch?v=1SUFMcYjCpE

## MVVM
https://benoitpasquier.com/how-to-use-rxtests-to-test-mvvm/




## Resources

Refer to the iOS/test folder for detailed documentation about my understanding of XCTests and work your way up from that basics towards RxSwift Testing

