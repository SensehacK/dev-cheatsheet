# Timer

```swift
let timer = Timer.scheduledTimer(timeInterval: 1.0, target: self, selector: #selector(fireTimer), userInfo: nil, repeats: true)


@objc func fireTimer() {
    print("Timer fired!")
}
```


Using DispatchQueue

```swift
DispatchQueue.main.asyncAfter(deadline: .now() + 1) {
    print("Timer fired!")
}
```

[Hacking with Swift Timer Ultimate guide](https://www.hackingwithswift.com/articles/117/the-ultimate-guide-to-timer)


[SO Elapsed time](https://stackoverflow.com/questions/24755558/measure-elapsed-time-in-swift)


## RxTimer

Using timer to continuesly check for certain condition - that could be the access token or refresh token expiring on app launch to present the login screen or logout the user for security purposes.
We can achieve that using a `timer` option in Rx world.
Method Signature
```swift
.timer(_ dueTime: RxTimeInterval, period: RxTimeInterval? = nil, scheduler: SchedulerType)
```

```swift

Observable<Int>
	.timer(initialTimerInterval, 
	period: refreshTokenInterval,
	scheduler: MainScheduler.asyncInstance)
	.filter { _ in filterVariable }
	.mapToVoid()
	.map { object }
	.bind(to: subject)
	.disposed(by: bag)


static let initialTimerInterval: RxTimeInterval = .milliseconds(400)
static let refreshTokenInterval: RxTimeInterval = .seconds(5)
```

Previous implementation had 
```swift
.interval(.seconds(Constant.refreshTokenInterval),
		  scheduler: MainScheduler.instance)
```

One of the main reasons to switch to timer from Interval would be start with timer option.
As stated by my teammate in an excellent MR changeset comment

```text
1.  it makes it clear that we're using a timer to drive the logic here rather than a more vague `interval`
2.  this method allows us to configure a timer with an initial event (the `dueTime` argument). this allows us to check for refresh token expiration at the start of the timer and then at regular time intervals after that (the `period` argument). without this, or if we continued using `Observable.interval`, we should need to introduce a `.startWith(0)` to this sequence to have it check for expiration when this sequence is created

Note: unfortunately we can't pass `.seconds(0)` as the `dueTime` as this prevents an initial element from being emitted and the use of `.startWith(0)` would again be required. so i just sent a sufficiently small time interval of 400 milliseconds
```
Which also states the `.startWith()` observable chain being ready for observing so to get around that we start with `.milliseconds(400)` 