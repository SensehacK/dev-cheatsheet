# Observable

## Intro

## Observable

It is a type of a property wrapper with syntax `@Observable`

### Code

```swift
@Observable
class CustomViewModel {
	 var data: [CustomData] = []
}
```

[Observation](https://developer.apple.com/documentation/Observation) support in SwiftUI is available starting with iOS 17, iPadOS 17, macOS 14, tvOS 17, and watchOS 10.

## ObservableObject
### Code

```swift
// View
@StateObject var model: CustomViewModel = CustomViewModel()


// View Model
class CustomViewModel: ObservableObject {
	@Published var data: [CustomData] = []
	
	func fetchRecipes() async {
		data = service.getData(serviceType: .privateAPI)
    }
}
```

## Migration

Switch from `ObservableObject` to `Observable` macro
[apple doc | Migrating from the Observable Object protocol to the Observable macro](https://developer.apple.com/documentation/swiftui/migrating-from-the-observable-object-protocol-to-the-observable-macro)


## Mind Map

No rxSwift equivalent, since in ReactiveIO,X you need to own your viewModel and make sure they are explicitly set whether they can be observed. With SwiftUI + Combine, you can just mark a class as conforming to `ObservableObject` and swift does internal markup of making sure which variables are annotated with `@Published` or `@State` etc.


## Errors

`ObservedObject` [initialized twice bug | SO post](https://stackoverflow.com/questions/59533407/swiftui-observableobject-created-multiple-times)


## References

[apple docs | managing model data](https://developer.apple.com/documentation/swiftui/managing-model-data-in-your-app)