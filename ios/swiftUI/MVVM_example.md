


```swift
// Model
struct Meal: Decodable {
    let strMeal: String
    let strMealThumb: String
    let idMeal: String
}

// View 
struct InternalView: View {
	var recipe: [RecipeData]
}

// View Controller
struct CustomListView: View {
	@StateObject var model: CustomViewModel = CustomViewModel()
	var body: some View {
		InternalView(recipe: model.data)
	}
}

// ViewModel
@MainActor
class CustomViewModel: ObservableObject {
	@Published var data: [MealViewModel] = []
	func fetchRecipes() async {
        do { let recipes = try await AsyncNetwork.shared.fetchData(url: Constants.API.mealURL, type: MealModel.self)
            meals = recipes.meals.map { MealViewModel(meal: $0) }
        } catch { print(error) }
    }
}

/// Consumable ViewModel
struct MealViewModel: Identifiable {
    fileprivate let meal: Meal
    init(meal: Meal) {
        self.meal = meal
    }
    var id: String { meal.idMeal }
    var title: String { meal.strMeal }
}


```

Network Async / Await
```swift
public func fetchData<T: Decodable>(url: String, id: Int? = nil, type: T.Type) async throws -> T {
        guard let url = URL(string: url) else {
            throw NetworkError.invalidURL
        }
        let (data, response) = try await URLSession.shared.data(from: url)
        guard let response = response as? HTTPURLResponse,
              response.isResponseOK() else {
            throw NetworkError.requestBad
        }
        guard let decodedData = try? JSONDecoder().decode(T.self, from: data) else {
            throw NetworkError.requestBadDecoding
        }
        return decodedData
    }
```


## Passing StateObject to Extracted View

Utilize @ObservedObject for passing ViewModel ref in extracted views.

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

Passing Data between Views in SwiftUI
https://www.createwithswift.com/tutorial-passing-data-between-views-in-swiftui-using-state-and-binding/

https://www.swiftdevjournal.com/passing-data-to-swiftui-views/

Pass `@StateObject` data in views.
https://www.hackingwithswift.com/books/ios-swiftui/sharing-swiftui-state-with-stateobject