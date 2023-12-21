# Thread

## Intro

Individual [tasks](tasks.md) runs on Thread with a priority assigned by the Operating system runtime operation.

## Syntax

Check whether the current thread is on `main` or background global instance.

```swift
print ("The current thread: \(Thread.current)")
```

## Dispatch Group

[dispatch_global](dispatch_global.md)

[Concurrency in iOS ](https://metova.com/concurrency-in-ios/)

## Dispatch Queue

Concurrent or Singular Synchronous
[dispatch_queue](dispatch_queue.md)

Main thread
[dispatch_main](dispatch_main.md)

## [Dispatch Work Item](dispatch_work_item.md)

## Race Condition

[SO| What is Race Condition](https://stackoverflow.com/questions/34510/what-is-a-race-condition?rq=1)

## Critical Section

## [Semaphores](dispatch_semaphore.md)

## [RxSwift threads](threads.md)


## Learn

More about race conditions and avoiding critical reads / writes sections in the memory at once.
Multithreading - checks for whether certain things needed to be checked for thread safety overall.
The interview basically asked me all the multithreaded questions which I didn't know an answer for.


## Good sources

[Free code camp Concurrency](https://www.freecodecamp.org/news/ios-concurrency/)

[async-await](https://www.avanderlee.com/swift/async-await/)

[advancedswift | /async-await/](https://www.advancedswift.com/async-await/)

[guide-to-operation-and-operationqueue](https://medium.com/swlh/an-in-depth-guide-to-operation-and-operationqueue-45658a22ee37)

[using-dispatch-async-to-load-images-in-background](https://www.appsloveworld.com/swift/100/174/using-dispatch-async-to-load-images-in-background)

[Apple Dev | Scheduler](https://developer.apple.com/documentation/combine/scheduler)

[Apple Dev | Runloop](https://developer.apple.com/documentation/foundation/runloop)