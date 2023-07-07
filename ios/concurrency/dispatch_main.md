# Dispatch Main

## Info

Serial Queue but async execution if `async` is being used. Usually the prefered option.
Usually needed for the system to switch threads 
eg. Network call -> Background thread
-> Jump/Transit to Main thread for UI updation tasks.


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



## MainActor

You can always define your class as an actor which would gurantee the reference type object to be in its own context with its dedicated thread.
It is Swift's newer APIs available for users to make it more thread safe and the general guidelines are to use `actor` if possible to avoid extra overhead of dealing with criticial section or putting barrier or signals when writing shared / mutable data / resource.

When using `Task { }` to perform any asynchronous task and utilizing the result of the async task to make some changes on UI, we need to again jump back to main thread. In order to do that sometimes SwiftUI is smart if the class is conforming to `:ObservableObject` and has `@mainActor` being marked it will do the thread switching in the background without explicit developer's input. But if using tasks and sending results back with completion handlers with closures. You need to be sure to premptively switch threads to the main thread for doing UI work.

```swift
Task {
do {
	let data = try await AsyncNetwork.shared.fetchData(url: url, type: User.self)
	await MainActor.run {
		completion(.success(data))
	}
} catch { print("error") }
}
```
The code snippet which makes sure we are on the main thread is `MainActor.run` , we can also use `DispatchQueue.main.async` block. But if we are already supporting async/await and using task might as well utilize the improved API.

## Actor

Refer this doc for more information [actors](actors.md)



## References

https://www.hackingwithswift.com/read/9/4/back-to-the-main-thread-dispatchqueuemain

https://holyswift.app/swift-and-combine-which-thread-runs-my-sink-closure/

https://www.avanderlee.com/combine/runloop-main-vs-dispatchqueue-main/

https://www.hackingwithswift.com/quick-start/concurrency/how-to-use-mainactor-to-run-code-on-the-main-queue