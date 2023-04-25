Serial queue
But background thread.
Only `Main` is the main thread which is kept for UI and `DispatchQueue.main`


QOS parameter.
5 different Quality of Service options

```swift
DispatchQueue.global().async {
	doSomething()
}
```