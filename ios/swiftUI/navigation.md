# Navigation

Turns out while interviewing, I couldn't recall what navigation syntax is used usually in swiftUI. 
Thankfully the interviewers encouraged me to use documentation. 
So just for future references for my navigation linking.

## Normal approach


```swift
NavigationView {
            List(favoritesStore.favorites, id: \.self) { favorite in
                NavigationLink(favorite) {
                    FavoriteDetailView(favorite: favorite)
                }
            }.navigationTitle("My Favorites")
        }
```

List with custom Cell view and destination navigation detail view
```swift
List(recipes) { recipe in
	NavigationLink(destination: DetailView(ID: recipe.id)) 
	{
		MealRecipeCellView(meal: recipe)
	}
}
```

NavigationLink should be inside the NavigationView just like how UIKit works with ViewController being part of the parent navigation ViewController.

```swift
NavigationView {
	VStack {
		Text("Hello World!")
		
		NavigationLink(destination: ViewInit()) {
			Text("Navigate to new screen")
		}
	}
}
```



## iOS 16

Navigation Stack - Router Based approach


## Binding Based approach



```swift
struct FavoritesProgrammaticallyView: View {

    @ObservedObject var favoritesStore: FavoritesStore = .standard

    /// Store the favorite that has to be shown inside a detail view.
    @State var selectedFavorite: String?

    var body: some View {
        NavigationView {
            List(favoritesStore.favorites, id: \.self) { favorite in
                Button(favorite) {

                    /// Update `selectedFavorite` on tap.
                    selectedFavorite = favorite
                }.tint(Color.primary)
            }.navigationTitle("My Favorites")

                /// Whenever `selectedFavorite` is set, a new `FavoriteDetailView` is pushed.
                .navigationDestination(for: $selectedFavorite) { favorite in
                    FavoriteDetailView(favorite: favorite)
                }
        }
    }
}
```


Source code snippets by [avanderlee](https://www.avanderlee.com/swiftui/navigationlink-programmatically-binding/)