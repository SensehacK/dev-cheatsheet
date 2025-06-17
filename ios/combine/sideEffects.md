
## Intro

copied

> You might be looking for the `.handleEvents` operator. You can implement it with any of five different parameters; they are all optional, so implement just those you need. Both an error and a completion would count as `receiveCompletion:`.

> Note that the error will still flow on down the pipeline if you don't `catch` it! (The completion will flow down the pipeline in any case, and I don't think you can stop it.)

[SO | rxswift combine side effect](https://stackoverflow.com/questions/62139342/performing-side-effects-on-publisher)



## Code

```swift
[1, 2, 3]
  .publisher
  .handleEvents(receiveSubscription: { _ in  
        print("Received subscription")  
    }, receiveOutput: { _ in  
        print("Received output")  
    }, receiveCompletion: { _ in  
        print("Received completion")  
    }, receiveCancel: {  
        print("Received cancel")  
    })
  .sink { number in
    print("Received value \(number)")
  }
  .store(at: &anyCancellable)
```