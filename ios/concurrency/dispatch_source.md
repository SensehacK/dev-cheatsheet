

## Intro

An object that coordinates the processing of specific low-level system events, such as file-system events, timers, and UNIX signals.


## Timer



```swift
let timerInterval = 3.00
private var queue = DispatchQueue(label: "com.player.TagTimer.queue",qos: .utility)

private let timer: DispatchSourceTimer = DispatchSource.makeTimerSource(queue: self.queue)

timer.setEventHandler { self.doSomethingAfterTimedOut()}
timer.schedule(deadline: .now() + timerInterval, repeating: timerInterval)
```

Starting resuming or stopping timers

```swift
timer.cancel()
timer.resume()
```

Be careful while cancelling a dispatch_object when its in a suspended state.

> Important
> It is a programmer error to release an object that is currently suspended, because suspension implies that there is still work to be done. Therefore, always balance calls to this method with a corresponding call to [`dispatch_resume`](https://developer.apple.com/documentation/dispatch/1452929-dispatch_resume) before disposing of the object. The behavior when releasing the last reference to a dispatch object while it is in a suspended state is undefined.

[apple docs | dispatch suspend](https://developer.apple.com/documentation/dispatch/1452801-dispatch_suspend)

## References


[apple docs | dispatch source](https://developer.apple.com/documentation/dispatch/dispatchsource)