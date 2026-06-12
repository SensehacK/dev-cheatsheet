

# Swift Testing

## Intro

New framework by apple which would be more expressive and is more aligned with what apple has started pushing for swift concurrency manifesto + macros in recent years.
For me it seems like a first party / class citizen treatment finally from apple to its testing framework tools.

## Code

## Renames

[apple | Migration guide](https://developer.apple.com/documentation/testing/migratingfromxctest)


## Test Throws


```swift
#expect(throws: URLParserPlayerError.self) {
	try urlResolver.isTemplateValid(resolverInput)
}
```

```swift
#expect {
	try urlResolver.isTemplateValid(resolverInput)
}
throws: { error in
	if let errorParsed = error as? URLParserPlayerError {
		#expect(errorParsed != nil)
		#expect(errorDescription == errorParsed.description)
	}
}
```

## Problems

### How to Wait

```swift
wait(for:timeout:)
```
[apple | wait](https://developer.apple.com/documentation/xctest/xctestcase/2806856-wait)




## Combine

Combine reactive paradigm testing with expectations to `confirmation`

```swift
@Test
func imageRetrieved() async {
  var cancellable: AnyCancellable?
  await confirmation { imageRetrieved in
    cancellable = viewModel.$image.dropFirst().sink { _ in
      // Do nothing on completion.
    } receiveValue: {
      #expect($0 != nil)
      imageRetrieved()
    }
  }
  cancellable?.cancel()
}
```

Converted to use `AsyncSequence` on the publishers

```swift
@Test
func imageRetrieved() async {
    let value = await viewModel.$image.values.first()
    #expect(value != nil)
}
```

With this extension to simplify the call to [`first(where:)`](https://developer.apple.com/documentation/swift/asyncsequence/first\(where:\)):

```swift
extension AsyncSequence {
    func first() async rethrows -> Element? {
        try await first(where: { _ in true})
    }
}
```

[SO | test combine publishers](https://stackoverflow.com/questions/79197294/how-to-test-combine-publishers-in-swift-testing)



## Parallelize 

Default all the unit tests are parallel. You can make the unit test serialized or all the unit tests in a specific class serialized.

All unit test
```swift
@Suite(.serialized)
struct EntosAdBeaconTests {
	@Test("test1")
    func test1() async { }
    
    @Test("test2")
    func test2() async { }
    
    @Test("test3")
    func test3() async { }
}
```

Specific unit test
```swift
@Test("test1", .serialized, arguments: [1, 3, 33, 69])
func testMultiple(values: Int) async { }
}
```

## Struct 

setupWithError() -> init() 
teardown() -> deinit()

```swift
struct AdBeaconTests : ~Copyable {
	init() async throws { }
	
	deinit { }
}
```

## Completion handler migration

[donnywals | testing-completion-handler-apis-with-swift-testing](https://www.donnywals.com/testing-completion-handler-apis-with-swift-testing/)
### XCTest

Mock Class

```swift
final class MockAdBeaconable: AdBeaconable {
    // define the expectation
    let expectation: XCTestExpectation
    var resultType: BeaconType? = nil
    
    init(expectation: XCTestExpectation,
	     resultType: BeaconType? = nil) {
		    self.expectation = expectation
		    self.resultType = resultType
    }

    // Callback from protocol DI
    func prepare(type: BeaconType) { 
        if type == resultType {
            expectation.fulfill()
        }
    }
}
```

unit test
```swift
final class AdExpectationTests: XCTestCase {
    func testExpectationOverload() {
        let expectation = self.expectation(description: "Expect fulfillment from one eligible segment")
        expectation.expectedFulfillmentCount = 1
        // expectation.isInverted = true
        
        let mockProvider = MockAdBeaconable(expectation: expectation)
        let resolver = LinearAdResolver(adProvider: mockProvider)

        // supply events
        Task {
            resolver.processSomeEvents(MockEvents.progress))
        }
        
        wait(for: [expectation], timeout: 3)
    }
}
```

### Swift Testing Continuation

Mock class conforming with DI protocol
```swift
final class MockAdBeaconable: AdBeaconable {
    var resultType: BeaconType? = nil
    // define the async continuation point
    private var continuation: CheckedContinuation<BeaconType, Never>?

    init(resultType: BeaconType? = nil) { }

    // Hang point
    func getBeacons() async -> BeaconType {
        await withCheckedContinuation { (continuation: CheckedContinuation<BeaconType, Never>) in
            self.continuation = continuation
        }
    }

    // Callback from protocol DI
    func prepare(type: BeaconType) { 
        if type == resultType {
            continuation?.resume(returning: type)
            continuation = nil
        }
    }
}
```



Unit test trying to utilize dependency injection, instead of using Wait for expectations, utilizing Continuation

```swift
@Test("Expectations fulfill to Continuation")
func waitExpectationWithContinuation() async { 
    // Initialize Dependency Injection wrapper
    let mockBeaconer = MockAdBeaconable(resultType: .adBreakStart)

    let adBeaconingManager = AdBeaconing(handler: mockBeaconer)

    // Initialize Event Bus
    let mockAdPlayerEventBus = MockAdBus(bus: mockEventBus)
    adBeaconingManager.configure(with: mockAdPlayerEventBus)

    // Send mock events
    mockAdPlayerEventBus.bus.send(mockEvent1)
    mockAdPlayerEventBus.bus.send(mockEvent2)

    // Wait for async blocking call
    let result = await mockBeaconer.getBeacons()

    // Assert / check
    #expect(result == .adBreakStart)
}
```

## XCTest Time wait

[apple docs](https://developer.apple.com/documentation/xctest/xctestcase/executiontimeallowance)
```swift
var executionTimeAllowance: TimeInterval { get set }
```

### old

```swift
final class DataHandlingTests: XCTestCase {
func test_loadNames() async {
	let expectation = XCTestExpectation(description: "long task")
	await fulfillment(of: [expectation], timeout: 60)
	}
}
```

```swift
final class DataHandlingTests: XCTestCase {
	override setUp() {
		self.executionTimeAllowance = 60
	}
}
```
### new

```swift
struct DataHandlingTests
@Test("loading", .timeLimit(.minutes(1)))
func test_loadNames() { }
```





## Reference

[swift with majid | swift testing basics](https://swiftwithmajid.com/2024/10/22/introducing-swift-testing-basics/)

[avanderlee | swift testing](https://www.avanderlee.com/swift-testing/introducing-expressive-apis/)