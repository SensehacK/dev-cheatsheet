


```swift
// View
struct CustomListView: View {
	@StateObject var model: CustomViewModel = CustomViewModel()
	var body: some View {
		InternalView(recipe: model.data)
	}
}
// 2nd Extracted View 
struct InternalView: View {
	var recipe: [RecipeData]
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

// Model
struct Meal: Decodable {
    let strMeal: String
    let strMealThumb: String
    let idMeal: String
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