# Operations

## Intro

Under the hood, it is implemented under GCD.

Heavy lifting
Abstraction on top of Dispatch Queue

## Code Snippet
```swift
let mainQueue = OperationQueue.main

let customQueue = OperationQueue()
customQueue.maxConcurrentOperationCount = 30
```

## Advantages

NSOperation advantages over GCD:

- Control On Operation
you can Pause, Cancel, Resume an NSOperation

- Dependencies
you can set up a dependency between two NSOperations
operation will not started until all of its dependencies return true for finished.

- State of Operation
can monitor the state of an operation or operation queue. ready ,executing or finished

- Max Number of Operation
you can specify the maximum number of queued operations that can run simultaneously


## NSOperation

Operation Queue

When to Go for GCD or NSOperation
when you want more control over queue (all above mentioned) use NSOperation and for simple cases where you want less overhead (you just want to do some work "into the background" with very little additional work) use GCD

### References

[choosing-between-nsoperation-and-grand-central-dispatch](https://cocoacasts.com/choosing-between-nsoperation-and-grand-central-dispatch/)

[nsthread-vs-gcd-vs-nsoperationqueue](http://iosinfopot.blogspot.in/2015/08/nsthread-vs-gcd-vs-nsoperationqueue.html)

[NSHipster | nsoperation](http://nshipster.com/nsoperation/)

[SO](https://stackoverflow.com/questions/10373331/nsoperation-vs-grand-central-dispatch)

[Detailed code](http://www.knowstack.com/swift-3-1-concurrency-operation-queue-grand-central-dispatch/)

