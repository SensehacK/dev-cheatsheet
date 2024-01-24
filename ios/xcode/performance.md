# Performance


## Optimization

We can optimize the build performance of any project so that it saves time rebuilding or cleaning the project and compiling all of the files under one project structure. 

By giving better context to the compiler or Xcode would result in faster builds, results and quick prototypes of the idea.

[Analyze Xcode build performance](https://www.avanderlee.com/optimization/analysing-build-performance-xcode/)


## Instruments

[instruments](instruments.md)


[Profiler](https://www.avanderlee.com/debugging/xcode-instruments-time-profiler/)

## Debug

View Debugging
[debug](debug.md)

## Image allocation

Good talk about Image allocation and how thumbnail and resized images could actually save us lot of CPU cycles.

## Caching

Utilizing NSCache or our own dictionary of caching solution is great to improve our performance.


## Diffable data source

When your data source is hashable or identifiable. You can have your model conform to protocols `identifiable` or `hashable` and provide our own hasher functions.
You can also conform to `comparable` which lets you run operators like `>, <, == ` on your custom models and not just the primitive types provided by swift or any programming language.

## Static vs Dynamic dispatch

Static always wins because it knows where it needs to be dispatched when referering to the witness table.



## Reference vs Value types

Know the right data structure to choose from when you're assuming how the app architecture is leaning towards modularization, concurrency heavy or just thin clients.
It would also affect how the application communitcation pattern is being deployed internally. It is observer pattern, closure based, delegates or fully reactive.

Swift internal implementation for small optimization if using non mutable value types. In this post with [Copy On Write example](ios/lifecycle/swift_types#Copy on Write (CoW))


## Measure

Xcode or swift llvm gives us lots of tools to measure our method execution time and features. You can find it in this file more about  [measure](measure.md) usage in testing.

### Measure execution in a function

```swift
let start = CFAbsoluteTimeGetCurrent()
// run your work
let diff = CFAbsoluteTimeGetCurrent() - start
print("Took \(diff) seconds")
```

```swift
func doSomething() { 
	// do heavy operation 
}

let clock = ContinuousClock()
let result = clock.measure(doSomething)
```

[apple dev | clock](https://developer.apple.com/documentation/swift/clock)


## Tips

[Raywenderlich performance tips](https://www.raywenderlich.com/2752-25-ios-app-performance-tips-tricks)

https://aglowiditsolutions.com/blog/ios-app-performance-optimization/

https://medium.com/strava-engineering/striving-for-ios-app-performance-ac2e1d4c29a2

https://www.hackingwithswift.com/example-code/system/measuring-execution-speed-using-cfabsolutetimegetcurrent

https://stackoverflow.com/questions/24755558/measure-elapsed-time-in-swift