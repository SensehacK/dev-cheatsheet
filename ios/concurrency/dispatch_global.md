# Dispatch Global



## Info

Serial queue
But background thread.
Only `Main` is the main thread which is kept for UI and `DispatchQueue.main`


## QOS 
Quality Of Service parameter.
5 different Quality of Service options



## UIKit
```swift
DispatchQueue.global().async {
	doSomething()
}
```


## Combine
```swift
.subscribe(on: DispatchQueue.global())

.receive(on: DispatchQueue.global())
```
