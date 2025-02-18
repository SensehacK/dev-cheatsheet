


## UIScreen Not accessible

This won't be accessible in `xrOS` because there are no bounds to calculate.
You can just isolate this logic with [wildcard checks](/ios/library/wildcard_checks#Check%20OS%20Support) specifically to avoid VisionOS.

```swift

#if !os(xrOS)
#if !os(visionOS)
#endif
```

Updated from `xrOS` to `visionOS`
[Updated swift docs](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/statements/#Conditional-Compilation-Block)


```swift
.frame(width: UIScreen.main.bounds.width, height: 200)
```

It was recommended to use `UIWindowScene` but I couldn't figure it out.



Previews have different syntax for VisionOS vs iPad / iOS

```swift
#Preview {
    ContentView()
}
```


```swift
#Preview(windowStyle: .automatic) {
    MainView()
}
```


## [Migration to visionOS](/ios/xcode/migration#VisionOS)

