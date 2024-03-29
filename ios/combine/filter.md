# Filter

## Mind Map

RxSwift equivalent [distinct](distinct.md)

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

[apple doc | compact map](https://developer.apple.com/documentation/combine/empty/compactmap(_:))

[when to use combine filter and compact map](https://cocoacasts.com/combine-essentials-when-to-use-combine-filter-and-compactmap-operators)
