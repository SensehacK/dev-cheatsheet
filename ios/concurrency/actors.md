
Reference type.
Single threaded.
Much better solution than relying on classes for concurrency.




## Swift UI

Data model - View Models with `: OBservableObject` conformance to the class `SwiftUIViewModel` should be annotated with `@MainActor` for switching back threads from background to main.
`@Publish var propertyValues` would be observed in `SwiftUI Struct some View` so it is very important that UI elements data refresh things happens on Main thread.

Lot of I/O, font rasterization, 60 vs 120 frames, response times, input delay, processing relies on Main thread. UI Kit is built solely on Main Thread to run UI Tasks and make them as efficient as possible. Without any hitches or dropped frames while scrolling or doing highly intensive tasks.


https://www.hackingwithswift.com/quick-start/concurrency/how-to-use-mainactor-to-run-code-on-the-main-queue

https://www.hackingwithswift.com/quick-start/concurrency/important-do-not-use-an-actor-for-your-swiftui-data-models


