

## Intro



## Custom Subscriber

```swift
// Custom Subscriber
class CountSubscriber: Subscriber {
    typealias Input = Int
    typealias Failure = Never
    var subscription: Subscription?

    // 1.
    func receive(subscription: Subscription) {
        print("subscribed")
        self.subscription = subscription
        subscription.request(.max(1))
    }

    // 2.
    func receive(_ input: Int) -> Subscribers.Demand {
        print("received \(input)")
        DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
            self.subscription?.request(.max(2))
        }
        return Subscribers.Demand.none
    }

    // 3.
    func receive(completion: Subscribers.Completion<Never>) {
    }
}

// Invoke
let subject = PassthroughSubject<Int, Never>()
let subscriber = CountSubscriber()
subject.subscribe(subscriber)
subject.send(1)
subject.send(2)

DispatchQueue.main.asyncAfter(deadline: .now() + 3) {
    self.subject.send(3)
    self.subject.send(4)
    self.subject.send(5)
}
```

```output
subscribed
received 1
received 3
received 4
```
## Throttle

```swift
cancellable = Timer.publish(every: 1.0, on: .main, in: .default)
        .autoconnect()
        .throttle(for: 3.0, scheduler: RunLoop.main, latest: true)
        .sink{ date in
            print("received \(date)")
        }
```

```output
received 2021-11-10 18:36:16 +0000
received 2021-11-10 18:36:19 +0000
received 2021-11-10 18:36:22 +0000
received 2021-11-10 18:36:25 +0000
```

## Debounce

```swift
cancellable = subject
    .debounce(for: .seconds(0.5), scheduler: RunLoop.main)
    .sink { value in
        print("received \(value)")
    }
subject.send(1)
subject.send(2)

DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
    self.subject.send(3)
    self.subject.send(4)
}
```

```output
received 2
received 4
```



## References

Code snippets from this below article
[back-pressure-in-combine](https://tanaschita.com/20211205-back-pressure-in-combine/)


[apple docs - back pressure](https://developer.apple.com/documentation/combine/processing-published-elements-with-subscribers#Apply-Back-Pressure-with-a-Custom-Subscriber)
