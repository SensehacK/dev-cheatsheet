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