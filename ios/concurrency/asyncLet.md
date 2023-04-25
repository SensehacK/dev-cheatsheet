

# Async Let

Important for kicking off new tasks and not waiting for async tasks to complete and then move to next line of code like a imperative programming paradigm.
You can utilize `async let` for kicking off request

```swift
async let doSomethingAsync()
```

Not await for all those asynchronous tasks.
```swift
try await [do_some_tasks]
```

Full code for easier consumption of a task.

Requires iOS 13 I believe since Swift concurrency manifesto is part of certain OS minimum version requirements. Of course Xcode is smart enough to let us know if we need to add those `@available` tags.
## Code

```swift
var imagesAsync: [UIImage] = []
func fetchDataAsync() {
	async let (imageData0, _) = try URLSession.shared.data(from: URL(string: imagesArr[0])!)
	async let (imageData1, _) = try URLSession.shared.data(from: URL(string: imagesArr[1])!)
	async let (imageData2, _) = try URLSession.shared.data(from: URL(string: imagesArr[2])!)
	async let (imageData3, _) = try URLSession.shared.data(from: URL(string: imagesArr[3])!)
	async let (imageData4, _) = try URLSession.shared.data(from: URL(string: imagesArr[4])!)

	imagesAsync.append(contentsOf: try await [imageData0, imageData1,imageData2,imageData3])
}

```