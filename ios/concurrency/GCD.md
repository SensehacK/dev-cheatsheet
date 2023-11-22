
# GCD

## Intro

Every queue is always First In First Out (FIFO) order. 
The queue itself could be on main thread or background thread with varying Quality of services.

[Wikipedia](https://en.wikipedia.org/wiki/Grand_Central_Dispatch) 

Refer `Main thread` [dispatch_main](dispatch_main.md)
Refer Background threads [dispatch_global](dispatch_global.md)

## low-level C-based API

NSOperation and NSOperationQueue are Objective-C classes.
NSOperationQueue is objective C wrapper over GCD. If you are using NSOperation, then you are implicitly using Grand Central Dispatch.

### Advantages

GCD advantage over NSOperation:
- implementation 
For GCD implementation is very light-weight
NSOperationQueue is complex and heavy-weight

### Main thread
```swift
DispatchQueue.main.async  { 
	self.tableView.reloadData()
}
```
### Background Threads
```swift
DispatchQueue.global(qos: .background).async {
	doSomething()
}
```

## References

https://developer.apple.com/videos/play/wwdc2015/718/

https://www.kodeco.com/books/concurrency-by-tutorials/v2.0/chapters/2-gcd-vs-operations