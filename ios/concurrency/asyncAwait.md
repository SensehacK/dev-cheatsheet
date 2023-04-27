

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

https://www.hackingwithswift.com/quick-start/concurrency/how-to-fix-the-error-async-call-in-a-function-that-does-not-support-concurrency