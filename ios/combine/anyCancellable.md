# Any Cancellable


RxSwift equivalent of [disposeBag](disposeBag.md)

```swift
class Name {
	var cancellable = Set<AnyCancellable>()
	func something() {
		publisher.sink { val in
	            self.mainLabel.text = val
	        }
	        .store(in: &cancellable)
	}
}
```

vs 
You can't use this code even though you're storing the value of `sink` return type `AnyCancellable`
```swift
let anycancel = publisher.sink { val in
		self.mainLabel.text = val
}
```

Since the closure is a function which is of type reference.
So it would just not hold the reference of self to even subscribe to the publisher. As we are still in function scope of `setupPublisherSubscriber`

Even though we didn't use [weak self] and opted for strong reference it won't subscribe unless the `AnyCancellable` returned by `sink` or `assign(to:)` isn't hold on class level reference.

This could be also attributed to Hot vs Cold observable phenomenon in RxSwift



## Links

https://www.avanderlee.com/swift/combine/


