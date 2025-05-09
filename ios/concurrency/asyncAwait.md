# Async Await

## Code

Swift Concurrency Manifesto

```swift
let (data, response) =  try await URLSession.shared.data(from: URL(string: "website.com")!)
```

## Wrap it in Task

```swift
func doAsyncWork() async {
    print("Doing async work")
}

func doRegularWork() {
    Task {
        await doAsyncWork()
    }
}

doRegularWork()
```

[how-to-fix-the-error-async-call-in-a-function-that-does-not-support-concurrency](https://www.hackingwithswift.com/quick-start/concurrency/how-to-fix-the-error-async-call-in-a-function-that-does-not-support-concurrency)


Make sure when you are returning from Task and if performing any UI operation. Switch back to the main thread using either `DispatchQueue.main` or `@MainActor` or `MainActor { }`
More information in this section [dispatch_main](/ios/concurrency/dispatch_main#MainActor)  

## Result from Task

```swift
func testWeatherAPIByCity() async -> [WeatherCity?] {
    let downloadCities = Task { () -> [WeatherCity?] in
        var cityArr: [WeatherCity?] = []
        async let city1 = getWeatherCityby(name: "Mumbai")
        async let city2 = getWeatherCityby(name: "London")
        async let city3 = getWeatherCityby(name: "Hyderabad")
        cityArr.append(contentsOf: await [city1, city2, city3])
        return cityArr
    }
    
    do {
        let result = try await downloadCities.result.get()
        return result
    } catch {}
    return []
}
```

[how-to-get-a-result-from-a-task](https://www.hackingwithswift.com/quick-start/concurrency/how-to-get-a-result-from-a-task)

## Memory Management

[memory-management-for-async-await](https://tanaschita.com/20221003-memory-management-for-async-await/)

## Resources

[swift-async-await matteomanferdini](https://matteomanferdini.com/swift-async-await/)
[async-await avanderlee](https://www.avanderlee.com/swift/async-await)