# Concurrency

If you want to get a refresher of basic concurrency concepts please read through the `os\architecture\concurrency.md` file. As this specifically discusses on Swift iOS / Apple SDK implementation code snippets.

## Threads Concurrency

## GCD is a low-level C-based API.
NSOperation and NSOperationQueue are Objective-C classes.
NSOperationQueue is objective C wrapper over GCD. If you are using NSOperation, then you are implicitly using Grand Central Dispatch.

GCD advantage over NSOperation:
i. implementation
For GCD implementation is very light-weight
NSOperationQueue is complex and heavy-weight

Main thread
```swift
DispatchQueue.main.async  { 
		self.tableView.reloadData()
}

DispatchQueue.global(qos: .background).async {

}

```

## NSOperation Operation Queue

NSOperation advantages over GCD:

i. Control On Operation
you can Pause, Cancel, Resume an NSOperation

ii. Dependencies
you can set up a dependency between two NSOperations
operation will not started until all of its dependencies return true for finished.

iii. State of Operation
can monitor the state of an operation or operation queue. ready ,executing or finished

iv. Max Number of Operation
you can specify the maximum number of queued operations that can run simultaneously

When to Go for GCD or NSOperation
when you want more control over queue (all above mentioned) use NSOperation and for simple cases where you want less overhead (you just want to do some work "into the background" with very little additional work) use GCD

ref:
https://cocoacasts.com/choosing-between-nsoperation-and-grand-central-dispatch/ http://iosinfopot.blogspot.in/2015/08/nsthread-vs-gcd-vs-nsoperationqueue.html 
http://nshipster.com/nsoperation/


[SO](https://stackoverflow.com/questions/10373331/nsoperation-vs-grand-central-dispatch)

[Detailed code](http://www.knowstack.com/swift-3-1-concurrency-operation-queue-grand-central-dispatch/)

## Operation Queue
Under the hood, it is implemented under GCD.

Heavy lifting
Abstraction on top of Dispatch Queue

```swift
let mainQueue = OperationQueue.main

let customQueue = OperationQueue()
customQueue.maxConcurrentOperationCount = 30
```


## Dispatch Group

let group = DispatchGroup()


group.enter()
group.leave()



group.notify(queue: .main, execute: {

})


[Concurrency in iOS ](https://metova.com/concurrency-in-ios/)



## Race Condition


[SO](https://stackoverflow.com/questions/34510/what-is-a-race-condition?rq=1)

## Semaphores

DispatchSemaphore

## Learn

More about race conditions and avoiding critical reads / writes sections in the memory at once.
Multithreading - checks for whether certain things needed to be checked for thread safety overall.
The interview basically asked me all the multithreaded questions which I didn't know an answer for.




## Good sources

[Free code camp Concurrency](https://www.freecodecamp.org/news/ios-concurrency/)

https://www.avanderlee.com/swift/async-await/

https://www.advancedswift.com/async-await/

https://medium.com/swlh/an-in-depth-guide-to-operation-and-operationqueue-45658a22ee37

https://www.appsloveworld.com/swift/100/174/using-dispatch-async-to-load-images-in-background