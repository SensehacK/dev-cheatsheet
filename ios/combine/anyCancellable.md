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

Weak, unowned and self in combine
https://trycombine.com/posts/self-weak-unowned/


##  Subscription lifecycle

Note
One thing I have observed while making my network manager code for Combine in its own file. If I use a weak reference in the `sink` block then the subscription weren't initialized. And the moment I use no capture list in the sink block, it automatically publishes all the changes in the reactive chain.

It is because maybe I'm accessing the combine function of a class instance in a function. Which limits its scope of class reference.
Because if I use a singleton instance of `Network Manager` it just works fine.
I think so after my 15 mins debugging, I believe because I create the reference of `NEtwork Manager` in a function scope of the consumer. The Arc or `anycancellables` is deinitializing itself or subscription is ending quickly.
`.print()` operator really helped how to narrow down the publisher - subscription chain internal events. 



## Links

https://www.avanderlee.com/swift/combine/

https://www.swiftbysundell.com/articles/combine-self-cancellable-memory-management/

https://www.donnywals.com/what-exactly-is-a-combine-anycancellable/

https://tanaschita.com/20220912-memory-management-in-combine/

