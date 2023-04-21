
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