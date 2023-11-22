# Dispatch Global

## Info

Serial queue
But background thread.
Only `Main` is the main thread which is kept for UI and `DispatchQueue.main`


## QOS 
Quality Of Service parameter.
5 different Quality of Service options

-   **userInteractive:** Used for animations, or updating UI.
    
-   **userInitiated:** Used for tasks like loading data from API, preventing the user from making interactions.

-  **default** : The default quality-of-service class.
-   **utility:** Used for tasks that do not need to be tracked by the user.
    
-   **background:** Used for tasks like saving data in the local database or any maintenance code which is not on high priority.
-   **unspecified**: The absence of a quality-of-service class.

## UIKit
```swift
DispatchQueue.global().async {
	doSomething()
}
```


## Combine
```swift
.subscribe(on: DispatchQueue.global())

.receive(on: DispatchQueue.global())
```

## Source

https://developer.apple.com/documentation/dispatch/dispatchqos/qosclass

https://www.swiftpal.io/articles/what-is-qos-quality-of-service-in-gcd-swift