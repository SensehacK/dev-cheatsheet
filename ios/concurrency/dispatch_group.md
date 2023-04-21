
```swift
let group = DispatchGroup()
// 1
group.enter() // Different tasks can enter 
group.leave()
// 2
group.enter()
group.leave()
// 3
group.enter() 
group.leave()

// This will only get called when all the 3 groups have leave.
group.notify(queue: .main, execute: {

})
```