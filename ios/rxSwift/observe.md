



## Background thread

```swift
Observable
.merge(isAuthorizedFirstViewLoad,
                isAuthorizedAfterFirstViewLoad)
.subscribe(on: ConcurrentDispatchQueueScheduler(queue: scanningQueue))
.observe(on: ConcurrentDispatchQueueScheduler(queue: scanningQueue))
```

this change was important. `subscribe` was only creating the subscription on a background thread. changing it to `observe` ensures that events are actually handled on the background thread. confirmed this using breakpoints in Xcode.

this comment was provided by my mentor. 
TODO: I need to confirm how did he verify the background thread or main thread part on RxSwift or does `.debug()` prints that information. 
Or do we have a helper method to identify which thread is the subscription being called upon.


Github similar issue (https://github.com/ReactiveX/RxSwift/issues/1778)

