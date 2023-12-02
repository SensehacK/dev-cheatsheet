
# Dispatch Group

## Creation

```swift
let group = DispatchGroup()
```


## Usage 

Enter and Leave group for every tasks.
Different tasks can `enter` and after their completion can `leave`.

```swift
// 1
group.enter() 
group.leave()
// 2
group.enter()
group.leave()
// 3
group.enter() 
group.leave()
```

## Completion of Group tasks

This will only get called when all the 3 or `n` groups have left.
Queue to listen is also important, to receive notification on `main thread` and then execute is block operation doing tasks in that closure chunk.

```swift
group.notify(queue: .main, execute: {
	doSomethingAfterCompletingChildGroupTasks()
})
```

