
## Code

```swift
`...` vs `..<`
```

## Closed


```swift
let closedRange = 1...100
let openRange = 
```


## Clamping

### precondition

Limit Range via a precondition - run time failure

```swift
let param = 24
precondition((0...20).contains(param))
// Precondition failed
```

[apple docs | precondition](<https://developer.apple.com/documentation/swift/precondition(_:_:file:line:)>)



### logic

```swift

a -> 4.2
b -> 0
c -> 5

// Keeps a range of `0...5`
let clamped = min(max(a, 0), 5)
```


### Extension

Extension of `Comparable/Strideable` similar to `ClosedRange.clamped(to:_) -> ClosedRange` from standard Swift library.

```swift
extension Comparable {
    func clamped(to limits: ClosedRange<Self>) -> Self {
        return min(max(self, limits.lowerBound), limits.upperBound)
    }
}

#if swift(<5.1)
extension Strideable where Stride: SignedInteger {
    func clamped(to limits: CountableClosedRange<Self>) -> Self {
        return min(max(self, limits.lowerBound), limits.upperBound)
    }
}
#endif
```

**Usage:**

```swift
15.clamped(to: 0...10) // returns 10
3.0.clamped(to: 0.0...10.0) // returns 3.0
"a".clamped(to: "g"..."y") // returns "g"

// this also works (thanks to Strideable extension)
let range: CountableClosedRange<Int> = 0...10
15.clamped(to: range) // returns 10
```


[Clamping example in swift | SO](https://stackoverflow.com/questions/36110620/standard-way-to-clamp-a-number-between-two-values-in-swift)


Kotlin coerce range like function
[playground to play with it](https://play.kotlinlang.org/#eyJ2ZXJzaW9uIjoiMi4wLjIwIiwicGxhdGZvcm0iOiJqYXZhIiwiYXJncyI6IiIsIm5vbmVNYXJrZXJzIjp0cnVlLCJ0aGVtZSI6ImlkZWEiLCJjb2RlIjoiaW1wb3J0IGphdmEudGltZS5EYXlPZldlZWtcbmltcG9ydCBrb3RsaW4udGVzdC5hc3NlcnRGYWlsc1dpdGhcbmltcG9ydCBrb3RsaW4ubWF0aC4qXG5cblxuZnVuIG1haW4oYXJnczogQXJyYXk8U3RyaW5nPikge1xuXG52YWwgd29ya2luZ0RheXMgPSAwLi4xMDBcbnByaW50bG4oODAuY29lcmNlSW4od29ya2luZ0RheXMpKSAvLyBXRURORVNEQVlcbnByaW50bG4oMTAxLmNvZXJjZUluKHdvcmtpbmdEYXlzKSkgLy8gRlJJREFZXG5cbnByaW50bG4oLTE2LmNvZXJjZUluKDAsIDEwMCkpIC8vIC0xNj8gSXQgc2hvdWxkIGJlIDAgcmlnaHQ/XG5cbnByaW50bG4oXCJtaW5pbXVtXCIpXG5wcmludGxuKG1pbigtMTAsIC04KSlcbnByaW50bG4obWF4KC0xMCwgLTgpKVxuXG5cbnByaW50bG4obWF4KDEwMCwgNzkpKVxuXG5cbi8vIHByaW50bG4obWF4KERheU9mV2Vlay5TQVRVUkRBWS5pc29EYXlOdW1iZXIsRGF5T2ZXZWVrLkZSSURBWS5pc29EYXlOdW1iZXIpKVxuXG5wcmludGxuKERheU9mV2Vlay5GUklEQVkuY29lcmNlSW4oRGF5T2ZXZWVrLlNBVFVSREFZLCBEYXlPZldlZWsuU1VOREFZKSkgLy8gU0FUVVJEQVlcblxucHJpbnRsbihcImNvZXJjZUluXCIpXG5wcmludGxuKDUuY29lcmNlSW4oNiwgNykpIC8vIFxucHJpbnRsbigtMTEuY29lcmNlSW4oLTgsIDcpKVxufSJ9)