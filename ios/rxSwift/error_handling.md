
# Error Handling


## Debug

You can po event chains as well in order to see how it pans through the code live


`po observer.onError(networkError)`

This will execute that instruction and also in the same way show how the error propagates into the rx stream chain.

## Pipe Errors

Simulate some events based on Observable being returned as error.


```swift
yetAnotherSubject
	.mapToVoid()
	.map { return NSError(domain: "test error 2", code: -1) }
	.bind(to: observingSubject)
	.disposed(by: disposeBag)
```

## Resources


https://airnauts.medium.com/rxswift-errors-done-right-5284f4d7c063
Github https://github.com/ReactiveX/RxSwift/issues/729

Rx Common issues https://infinum.com/handbook/ios/rx/common-issues

Handle errors in RxSwift http://adamborek.com/how-to-handle-errors-in-rxswift/

SO https://stackoverflow.com/questions/46988049/rxswift-observable-error-stops-chain-web-services-with-rx-how-to-recover

