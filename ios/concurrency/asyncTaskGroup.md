# Async TaskGroup

Important for kicking off new tasks and not waiting for async tasks to complete and then move to next line of code like a imperative programming paradigm.
You can utilize `async let` for kicking off request

For TaskGroup with throwing tasks.
```swift
withThrowingTaskGroup(of: Type.self) 
```

Add these async tasks to the execution scheduler `group: TaskGroup`.
```swift
group.addTask {
    try await doSomeAsyncTask()
}
```
Usually good idea to iterate over the array of data to pull concurrent tasks which are not dependent on each other and are mutually exclusive.

## Code

Full code for easier consumption of a task.

```swift
func fetchImagesTaskGroup() async {
    if let images = try? await fetchImagesAsyncTaskGroup() {
        self.imagesAsyncGroup.append(contentsOf: images)
    }
}

func fetchImagesAsyncTaskGroup() async throws -> [UIImage] {
    return try await withThrowingTaskGroup(of: UIImage?.self) { [weak self] group in
        guard let self = self else { throw error }
        var images: [UIImage] = []
        images.reserveCapacity(imagesArr.count)
        for imageURL in imagesArr {
            group.addTask {
                try await self.fetchSingleImage(url: imageURL)
            }
        }

        for try await image in group {
            if let image = image { images.append(image) }
        }
        return images
    }
}

func fetchSingleImage(url: String) async throws -> UIImage {
    guard let url = URL(string: url) else { throw URLError(.badURL) }
    let (data, _) = try await URLSession.shared.data(from: url)
    guard let image = UIImage(data: data) else { throw error }
    return image
}

```

## Failing task in multiple tasks

You can also utilize optionals for your `Type` when we want to still proceed with running asynchronous tasks results.

Like `Type?.self` to denote that out of `n` network request one can fail and you don't want that failure to interrupt or infinitely wait out for getting results or fire more chain events dependent on a result. Swift strictly typed language gives us a way to properly harness that with defining optionality. Adhering internally to `ExpressibleByNil` protocol.

```swift
withThrowingTaskGroup(of: CustomModel?.self) 
```

## Order guarantee

Guaranteeing the order of async execution is important.
Easier solution is to use a dictionary to do unique Key mapping and then depending on what you want at the end of the async function you could return a dictionary or ordered array.
It would of course add one more `O(n)` complexity towards the creation of sorted array again from the dictionary.

Code snippet from [SO post](https://stackoverflow.com/a/69981562/17303441)

```swift
let stooges = ["moe", "larry", "curly"]
let images = await downloadImages(names: stooges)

imageView1.image = images["moe"]
imageView2.image = images["larry"]
imageView3.image = images["curly"]

func downloadImages(names: [String]) async -> [UIImage] {
    await withTaskGroup(of: (String, UIImage).self) { [self] group in
        for name in names {
            group.addTask { await (name, downloadPhoto(named: name)) }
        }

        let dictionary = await group.reduce(into: [:]) { $0[$1.0] = $1.1 }
        return names.compactMap { dictionary[$0] }
    }
}
```


Or you can also use tuples while making the `.addTask { }` call

```swift
let countries = await Server.shared.getCountries()
print(countries)
var capitals = [(country:String, capital:String)]()
await withTaskGroup(of: (String,String).self) { group in
    for country in countries {
        group.addTask {
            let capital = await Server
                                .shared
                                .getCapital(of:country)
            return (country,capital)
        }
    }
    for await pair in group {
        capitals.append(pair)
    }
}
print(capitals)
```

Good article about maintaining order in [async concurrent loops](https://www.swiftbysundell.com/articles/async-and-concurrent-forEach-and-map/).

## Async Loops

[asynchronous-looping-with-async-await](https://www.biteinteractive.com/swift-5-5-asynchronous-looping-with-async-await/)

[how-to-loop-over-an-asyncsequence-using-for-await](https://www.hackingwithswift.com/quick-start/concurrency/how-to-loop-over-an-asyncsequence-using-for-await)

## Handling Errors in TaskGroup

[task-groups-error-handling](https://swiftsenpai.com/swift/task-groups-error-handling/)
