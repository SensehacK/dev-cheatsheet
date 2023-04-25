# Dispatch Queue

## Intro

Default is always Serial Queue, unless you pass an attribute `.concurrent` in its initializer.
Then you have a concurrent queue.

## Code

```swift
// Normal Concurrent Queue
let customQueue = DispatchQueue(label: "com.sensehack.kautilya", attributes: .concurrent)

customQueue.async {
	doSomething()
}
```