# Actors

## Intro

Reference type.
Single threaded.
Much better solution than relying on classes for concurrency.

## New Kid on the Block

Reference type just like `Class` and `function` but it guarantees exclusive access to its execution environment with independent threads. Of course it does have to maintain references and the `reference` type checks and all that goody / baddy stuff for updating states across all the layers whenever something changes due to it inherently being of `reference` type but still great for Swift concurrency manifesto and not worrying about one more extra thing.

SwiftUI `ObservableObject` conforming classes can be marked with 
`@MainActor` and it just works like magic.
[actors | avanderlee](https://www.avanderlee.com/swift/actors/)

## Swift UI

Data model - View Models with `: ObservableObject` conformance to the class `SwiftUIViewModel` should be annotated with `@MainActor` for switching back threads from background to main.
`@Publish var propertyValues` would be observed in `SwiftUI Struct some View` so it is very important that UI elements data refresh things happens on Main thread.

Lot of I/O, font rasterization, 60 vs 120 frames, response times, input delay, processing relies on Main thread. UI Kit is built solely on Main Thread to run UI Tasks and make them as efficient as possible. Without any hitches or dropped frames while scrolling or doing highly intensive tasks.

[how-to-use-mainactor-to-run-code-on-the-main-queue](https://www.hackingwithswift.com/quick-start/concurrency/how-to-use-mainactor-to-run-code-on-the-main-queue)

[important-do-not-use-an-actor-for-your-swiftui-data-models](https://www.hackingwithswift.com/quick-start/concurrency/important-do-not-use-an-actor-for-your-swiftui-data-models)

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

[how-do-i-initialize-a-global-variable-with-mainactor](https://stackoverflow.com/questions/69263941/how-do-i-initialize-a-global-variable-with-mainactor)


## MainActor

You can always define your class as an actor which would gurantee the reference type object to be in its own context with its dedicated thread.
It is Swift's newer APIs available for users to make it more thread safe and the general guidelines are to use `actor` if possible to avoid extra overhead of dealing with critical section or putting barrier or signals when writing shared / mutable data / resource.

When using `Task { }` to perform any asynchronous task and utilizing the result of the async task to make some changes on UI, we need to again jump back to main thread. In order to do that sometimes SwiftUI is smart if the class is conforming to `:ObservableObject` and has `@mainActor` being marked it will do the thread switching in the background without explicit developer's input. But if using tasks and sending results back with completion handlers with closures. You need to be sure to preemptively switch threads to the main thread for doing UI work.

```swift
Task {
do {
    let data = try await AsyncNetwork.shared.fetchData(url: url, type: User.self)
    await MainActor.run {
        completion(.success(data))
    }
} catch { print("error") }
}
```

The code snippet which makes sure we are on the main thread is `MainActor.run` , we can also use `DispatchQueue.main.async` block. But if we are already supporting async/await and using task might as well utilize the improved API.

## Actor vs MainActor

[mainactor-dispatch-main-thread](https://www.avanderlee.com/swift/mainactor-dispatch-main-thread)

## References

[wwdc2021/10133](https://developer.apple.com/videos/play/wwdc2021/10133)

[wwdc2021/10254](https://developer.apple.com/videos/play/wwdc2021/10254)

[wwdc2021/10194](https://developer.apple.com/videos/play/wwdc2021/10194)
