

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


## Reference

[swift with majid | swift testing basics](https://swiftwithmajid.com/2024/10/22/introducing-swift-testing-basics/)

[avanderlee | swift testing](https://www.avanderlee.com/swift-testing/introducing-expressive-apis/)