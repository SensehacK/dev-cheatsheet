# Subject

## CurrentValueSubject

Holds the current value of the type defined. 
`CurrentValueSubject` is similar to `BehaviorRelay` where a single value is persisted with the subject instance and passed along during the event broadcast.
`CurrentValueSubject` is suitable for state

Below analogy by a fellow Stack overflow user - link in reference.

```text
**CurrentValueSubject = A light switch** Someone turns on the lights in your home when you are outside. You get back home and you know someone has turned them on.

CurrentValueSubject has an initial state, it retains the data you put in as its state.
```

### Initialization 

```swift
private let subject: CurrentValueSubject<String, Never>
var output: String = ""
```

### Sending values

```swift
subject.value = "Kautilya"
subject.value = "Sensehack"
subject.send(completion: .finished)
```

### Subscription

You can subscribe to the subject for its values and listen to them in a stream.

```swift
subject
	.dropFirst()
	.map { String("Hello \($0)" }
	.assign(to: &output)
```

The reason we start the pipeline by calling `dropFirst` is because a `CurrentValueSubject` emits its current value when a subscription is attached to it. Since that’ll always be an empty `subject` string in this case, we’re simply ignoring it.

## Quirks

### UIKit

Well suited for UIKit + Combine.
`didSet` internally it calls so that UIKit or subscribers can make the necessary changes with `CurrentValueSubject` value and it behaves differently compared to `@Publisher`. [publisher](publisher.md)

### Initialization Optionals

If we just define the current value subject with optional then it won't subscribe. 

Wrong Way
```swift
var users: CurrentValueSubject<UsersConsumableViewModel?, Error>
```

Right Way
```swift
var users = CurrentValueSubject<UsersConsumableViewModel?, Error>(nil)
```

It needs to be initialized with something in order for its subscribers to listen to its state. Another 18 mins spent around debugging and understanding why my data doesn't appear on the screen.
I love reactive paradigm and chasing its bugs asynchronously.

## PassthroughValueSubject

Holds the no initial value of the type defined. 
`PassThroughSubject` is like `PublishSubject` 
`PassthroughSubject` is suitable for event like tap action

Analogy by a fellow Stack overflow user - link in reference.

```text
**PassthroughSubject = A doorbell push button**

When someone rings the door, you are notified only if you are at home (you are the subscriber)

PassthroughSubject doesn't have a state, it emits whatever it receives to its subscribers.
```


### Initialization

```swift
var passthrough = PassthroughSubject<Int, Never>()
var numberString: String = ""
```
### Sending values
Can't use `passthrough.value = 5` 

```swift
passthrough.send(1)
passthrough.send(2)
```

### Subscription

You can subscribe to the subject for its values and listen to them in a stream.
The sink will only be called for values that are emitted after you subscribe.

```swift
passthrough
	.map { String("Number \($0)" }
	.sink(receiveValue: { print($0) })
	.store(in: &anyCancellables)
```

## Reference

https://stackoverflow.com/a/63404168/5177704

https://www.avanderlee.com/combine/passthroughsubject-currentvaluesubject-explained/


https://www.avanderlee.com/swiftui/published-property-wrapper/