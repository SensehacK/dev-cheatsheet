# Filter

## Mind Map

RxSwift equivalent [distinct](distinct.md)


## Basic Filter

1st approach

```swift
enum URLType: Equatable {
    case parse(URL)
    case resolve(URL)
}

let url: URLType = .parse(URL())

.filter { url in
	if case .parse(_) = url {
		return true
	} else { return false }
}
```

2nd Approach

```swift
extension URLType {
    var isParsed: Bool {
        if case .parse(_) = self { return true }
        return false
    }
}

.filter { $0.isParsed }
```


## Remove Duplicates

`.removeDuplicates()` this could be used on observer upstream chain and whatever values are coming down in the pipe needs to be conforming to protocol `equatable` or you can describe its closure to make small comparisons in the block.
Maybe it can automatically conform to `Equatable` when the model is already conforming to `Identifiable` since internally Apple can make hash comparison which needs unique elements. Don't know but would dig deep into it the next time I need to do filtering based on the value types.

```swift
struct CustomModel: Codable, Equatable {
	static func == (lhs: WeatherCity, rhs: WeatherCity) -> Bool {
        lhs.id == rhs.id // Or anything else
    }
}
```

[apple doc | removeDuplicates](https://developer.apple.com/documentation/combine/publisher/removeduplicates()) 

## Distinct Until

DistinctUntil changed equivalent of RxSwift ?

## Compact Map

```swift
urlOrchestrator.output.result
	.sink { [weak self] urlValue in
		switch urlResult {             
		case .success(let urlType):
			if case .parsed(let urlValue) = urlType {
	self?.urlOrchestrator?.input.type.send(.resolve(urlValue))
			}
		case .failure(let error):
			if let playerError = error as? PlayerError {
				self?.handleURLResolverFailure(playerError)
			}
		}
	}
	.store(in: &cancellables)
```
Converted to a filter and compact map.

```swift
urlOrchestrator.output.result
	.filter{ $0.isSuccess }
	.map { urlResult -> URLTypeResult?  in
		guard case let .success(urlType) = urlResult,
			  urlType.isParsed else { return nil }
		return urlType
	}
	.compactMap { $0?.getURL as? URL }
	.sink { [weak self] urlValue in           self?.urlOrchestrator?.input.type.send(.resolve(urlValue))
    }
            .store(in: &cancellables)

// Extensions on Enum
public enum URLTypeResult {
    case parsed(URL)
    case resolved(URL)
    
    public func getURL() -> URL {
            switch self {
            case .parsed(let url), .resolved(let url):
                return url
            }
    }
}
```


`Result.isSuccess` [result extension](result.md#Extension)

[apple doc | compact map](https://developer.apple.com/documentation/combine/empty/compactmap(_:))

[when to use combine filter and compact map](https://cocoacasts.com/combine-essentials-when-to-use-combine-filter-and-compactmap-operators)



## Soft Unwrap guard conditions

Previous code 

```swift
subscription = bus.errors
	.filter { $0.type == .playerItemStatusChanged }
	.sink { event in
		// filtering out for desired event type here
		guard let error = event.data?.error as? NSError,
			  let itemError = self.playerItem.error as? NSError else { return }
		XCTAssertEqual(event.data?.playerItemStatus, .failed)
		XCTAssertEqual(error.domain, itemError.domain)
		XCTAssertEqual(error.code, itemError.code)
		expectation.fulfill()
	}
```

Newer code
```swift
subscription = bus.errors
	.filter { $0.type == .playerItemStatusChanged }
	.compactMap { engineErr -> (AVPlayerItem.Status, NSError, NSError)? in
		guard let engineD = engineErr.data,
			  let error = engineD.error as? NSError,
			  let itemError = self.playerItem.error as? NSError,
			  let engItemStatus = engineD.playerItemStatus else { return nil }
		return (engItemStatus, error, itemError)
	}
	.sink { (engineD, nsError, itemErr) in
		XCTAssertEqual(engineD, .failed)
		XCTAssertEqual(nsError.domain, itemErr.domain)
		XCTAssertEqual(nsError.code, itemErr.code)
		expectation.fulfill()
```


## References

[Parse dont validate](https://lexi-lambda.github.io/blog/2019/11/05/parse-don-t-validate/)