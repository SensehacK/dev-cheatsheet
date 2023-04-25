# Dispatch Main
## Info

Serial Queue but async execution if `async` is being used. Usually the prefered option.
Usually needed for the system to switch threads 
eg. Network call -> Background thread
-> Jump/Transit to Main thread for UI updation tasks.


## UIKit
```swift
DispatchQueue.main.async  {
	self.tableView.reloadData()
}
```


## Combine
```swift
.receive(on: Runloop.main)

.receive(on: Main.asyncInstance)
```

## RxSwift

```swift
.subscribeOn(MainScheduler.instance)
```

## SwiftUI

```swift
@MainActor
class CustomClass: ObservableObject {
	@Published var data: [Data] = []

	init() { fetchData() }

	func fetchData() {
		
		data = await URLSession.shared.data(url: "https://sensehack.github.io/")
	}
}
```
