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