# MVVM High Level example


## Model

```swift
struct Meal: Decodable {
    let strMeal: String
    let strMealThumb: String
    let idMeal: String
}
```

## View

This could be part of the ViewController + View 
```swift
struct CustomListView: View {
	@StateObject var model: CustomViewModel = CustomViewModel()
	var body: some View {
		InternalView(recipe: model.data)
	}
}
```

### Extracted View 

```swift
struct InternalView: View {
	var recipe: [RecipeData]
}
```

## ViewModel

You can inject any implementation as long as it conforms to protocol.
Great for dependency injection and adding a facade pattern to the init. Now the view controller or View won't have to change every time we change our internal API dependencies to get the concrete type of data. We can always be sure that the interface protocol method signature will stay the same irrespective of internal implementation changes. Abstraction at its best and easily able to loosely coupled the ViewModel , View and Service + Network implementation. 
This could be also testable with Mocking CustomViewServiceable.

```swift
@MainActor
class CustomViewModel: ObservableObject {
	@Published var data: [MealViewModel] = []
	let service: CustomViewServiceable

	
	init(serviceImplementation: CustomViewServiceable) {
		service = serviceImplementation
	}
	func fetchRecipes() async {
		data = service.getData(serviceType: .privateAPI)
    }
}
```

read more about [observable](observable.md)


## Modular - Loosely Coupled

### Consumable ViewModel
```swift
struct MealViewModel: Identifiable {
    fileprivate let meal: Meal
    init(meal: Meal) {
        self.meal = meal
    }
    var id: String { meal.idMeal }
    var title: String { meal.strMeal }
}
```

### Enum

```swift
enum CustomViewServiceType {
	case otherAPI
	case privateAPI
}
```
### Protocol 

```swift
protocol CustomViewServiceable {
	func getData(serviceType: CustomViewServiceType) -> MealViewModel
}
```


### CustomList Service

The actual magic of keeping it loosely coupled. We can route any input via the protocol conformance `getData` method and internally can switch endpoints or do anything to create those ViewModel objects and send it back.

```swift

class CustomViewService: CustomViewServiceable {
	func getData(serviceType: CustomViewServiceType)  -> MealViewModel {
		 var mealViewModel
		 switch serviceType {
		 case .otherAPI: 
			 let response = getDataOtherAPI()
			 // Parse that response into `MealViewModel` type
		 case .privateAPI: 
			 let response = getDataPrivateAPI()
			 // Parse that response into `MealViewModel` type
		 }
		let mealViewModel = parseNetworkResponseToViewModel(serviceType)
		return mealViewModel
	}

	private func getDataPrivateAPI() -> ResponseType {
		do { 
			 let recipes = try await AsyncNetwork
			 .shared
			 .fetchData(url: Constants.API.mealURL, type: MealModel.self
			 
			 return recipes.meals.map { MealViewModel(meal: $0) }
        } catch { print(error) }
	}
	
	private func getDataOtherAPI() -> ResponseType {
		// Make network request
	}

	private func parseNetworkResponseToViewModel(type: CustomViewServiceType) -> MealViewModel {
		// do conditional ViewModel creation based on Enum and associated response types.
		
	}
}
```

## Generic Network Async / Await

```swift
public func fetchData<T: Decodable>(url: String, id: Int? = nil, type: T.Type) async throws -> T {
        guard let url = URL(string: url) else {
            throw NetworkError.invalidURL
        }
        let (data, response) = try await URLSession.shared.data(from: url)
        guard let response = response as? HTTPURLResponse,
              (200..<300).contains(httpResponse.statusCode) else {
            throw NetworkError.requestBad
        }
        guard let decodedData = try? JSONDecoder().decode(T.self, from: data) else {
            throw NetworkError.requestBadDecoding
        }
        return decodedData
    }
```


## Modular Views

Passing StateObject to Extracted View
Utilize `@ObservedObject` for passing ViewModel ref in extracted views.

```swift
struct ContentView: View {
    @StateObject var vm = ViewModel()
	var body {
		ExtractedView(vm: vm)
	}
}

struct ExtractedView: View {
	@ObservedObject var vm: ImageNetwork

	// do something
	VStack { 
		Text(vm.fetchText())
	}
}
```



## Error Enums

```swift
enum NetworkError: Error {
    case requestBad
    case requestDataFailedNetworkError
    case invalidURL
    case requestBadDecoding
    case unknown
}
```


## References 

Passing Data between Views in SwiftUI
[tutorial-passing-data-between-views-in-swiftui-using-state-and-binding](https://www.createwithswift.com/tutorial-passing-data-between-views-in-swiftui-using-state-and-binding/)

[swift dev journal | passing-data-to-swiftui-views](https://www.swiftdevjournal.com/passing-data-to-swiftui-views/)


Pass `@StateObject` data in views.

[HWS | sharing-swiftui-state-with-stateobject](https://www.hackingwithswift.com/books/ios-swiftui/sharing-swiftui-state-with-stateobject)
