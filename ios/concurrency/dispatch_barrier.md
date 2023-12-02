# Dispatch Barrier

## Custom Concurrent Queue

```swift
// Normal Concurrent Queue
let customQueue = DispatchQueue(label: "com.sensehack.kautilya", attributes: .concurrent)

customQueue.async(flags: .barrier) {
    doSomething()
}

```

Flag: `barrier` is being set to signal the executioner that this part of async block of code is critical and you need have a barrier in place in order to not make unexpected behavior and only execute it if it has exclusive access.


## Dispatch Background Queue

```swift
DispatchQueue.global().sync(flags: .barrier) {
    doSomething()
}
```
