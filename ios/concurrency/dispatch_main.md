# Dispatch Main

## Info

Serial Queue but async execution if `async` is being used. Usually the prefered option.
Usually needed for the system to switch threads 
eg. Network call -> Background thread
-> Jump/Transit to Main thread for UI updating tasks.


### Warnings

Xcode by default has main thread checker enabled which is a good thing and lets us quickly fix the issue while building the project using simulators.

Settings could be found in  Xcode Product scheme -> Run -> Diagnostics ->
`Main thread Checker` 

Publishing changes from background threads is not allowed; make sure to publish values from the main thread (via operators like receive(on:)) on model updates.

## UIKit

```swift
DispatchQueue.main.async  {
	self.tableView.reloadData()
}
```


## Combine

Read more about [combine thread](receive_on.md)

### Publishers
Sending values from Publishers

```swift
.subscribe(on: DispatchQueue.global())
```

### Subscriber

Sink receive values when we are subscriber / observer

```swift
.receive(on: Runloop.main) 

.receive(on: DispatchQueue.main)
```


Runloop.main - User interaction | UI gestures will pause changes | execution of code 

```text
Updating your UI while scrolling might affect the frames per second (FPS) and smooth scrolling. It could be that your UI update isn’t as necessary when the user is scrolling. In that case, it might make sense to opt-in to using RunLoop.main as a scheduler. - avanderlee
```


DispatchQueue.main - User interaction won't pause the execution.

## RxSwift

RxSwift equivalents [[Observe]]

### Observe Publisher

```swift
.subscribe(on: MainScheduler.instance)
.subscribe(on: MainScheduler.asyncInstance)
```

### Subscriber / Observer

```swift
.observe(on: MainScheduler.asyncInstance)
.observe(on: MainScheduler.instance)
```
Custom Queue scheduler
```swift
let scheduler = SerialDispatchQueueScheduler(queue: DispatchQueue.main, internalSerialQueueName: "CustomQueue")
.observe(on: scheduler)
```

## SwiftUI

```swift
@MainActor
class CustomClass: ObservableObject {
	@Published var data: [Data] = []

	init() { fetchData() }

	func fetchData() {
		
		data = await URLSession.shared.data(url: "https://sensehack.github.io/")
	}
}
```




## Actor & MainActor

Refer this doc for more information
[actors](actors.md)
[main actor](actors.md##MainActor)

## References
[HWS | back-to-the-main-thread-dispatch queue main](https://www.hackingwithswift.com/read/9/4/back-to-the-main-thread-dispatchqueuemain)

[Avanderlee | runloop-main-vs-dispatchqueue-main](https://www.avanderlee.com/combine/runloop-main-vs-dispatchqueue-main/)
