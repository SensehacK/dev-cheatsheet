# Actors

## Intro

Reference type.
Single threaded.
Much better solution than relying on classes for concurrency.

## New Kid on the Block

Reference type just like `Class` and `function` but it guarantees exclusive access to its execution environment with independent threads. Of course it does have to maintain references and the `reference` type checks and all that goody / baddy stuff for updating states across all the layers whenever something changes due to it inherently being of `reference` type but still great for Swift concurrency manifesto and not worrying about one more extra thing.

SwiftUI `ObservableObject` conforming classes can be marked with 
`@MainActor` and it just works like magic.

https://www.avanderlee.com/swift/actors/

## Swift UI

Data model - View Models with `: ObservableObject` conformance to the class `SwiftUIViewModel` should be annotated with `@MainActor` for switching back threads from background to main.
`@Publish var propertyValues` would be observed in `SwiftUI Struct some View` so it is very important that UI elements data refresh things happens on Main thread.

Lot of I/O, font rasterization, 60 vs 120 frames, response times, input delay, processing relies on Main thread. UI Kit is built solely on Main Thread to run UI Tasks and make them as efficient as possible. Without any hitches or dropped frames while scrolling or doing highly intensive tasks.


https://www.hackingwithswift.com/quick-start/concurrency/how-to-use-mainactor-to-run-code-on-the-main-queue

https://www.hackingwithswift.com/quick-start/concurrency/important-do-not-use-an-actor-for-your-swiftui-data-models


## Global variable as Main actor

Code snippet from the SO post linked below. Interesting things.


One way would be to store the variable within a container (like an `enum` acting as an abstract namespace) and also isolating this to the main actor.

```swift
@MainActor
enum Globals {
  static var foo = Foo()
}
```

An equally valid way would be to have a "singleton-like" `static` property on the object itself, which serves the same purpose but without the additional object.

```swift
@MainActor
struct Foo {
  static var shared = Foo()
}
```

You now access the global object via `Foo.global`.

One thing to note is that this will now be lazily initialized (on the first invocation) rather than immediately initialized. You can however force an initialization early on by making any access to the object.

```swift
// somewhere early on
_ = Foo.shared
```

https://stackoverflow.com/questions/69263941/how-do-i-initialize-a-global-variable-with-mainactor



## Actor vs MainActor

https://www.avanderlee.com/swift/mainactor-dispatch-main-thread/

## References


https://developer.apple.com/videos/play/wwdc2021/10133

https://developer.apple.com/videos/play/wwdc2021/10254/

https://developer.apple.com/videos/play/wwdc2021/10194