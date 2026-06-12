
## Description

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


## nonisolatedfunc main actor


How to Access MainActor-isolated Properties from a Nonisolated Function
To safely access or modify a `MainActor`-isolated property from a `nonisolated` function, you must explicitly hop to the `MainActor`'s execution context. This is achieved using `await MainActor.run { ... }` or by calling an `async` function that is itself `MainActor`-isolated.


```swift
@MainActor
class ViewModel {
    var data: String = "Initial Data"
    func updateUI() { }
}


func processData(viewModel: ViewModel) async {
    // This is a nonisolated function

    // Cannot directly access viewModel.data here:
    // viewModel.data = "New Data" // ERROR: Main actor-isolated property 'data' can not be referenced from a nonisolated context

    // Safely update MainActor-isolated property by hopping to MainActor
    await MainActor.run {
        viewModel.data = "New Data"
        viewModel.updateUI() // Call MainActor-isolated method
    }
}

```