




Working with Identifiable
https://www.hackingwithswift.com/books/ios-swiftui/working-with-identifiable-items-in-swiftui


```swift


let model: MealRecipeDetailViewModel

    let gridItems = [

        GridItem(.adaptive(minimum: 60))

    ]

    var body: some View {

        VStack {

            Text(Constants.ingredients)

                .font(.headline)

            LazyVGrid(columns: gridItems, alignment: .center) {

                ForEach(model.recipeMeal.ingredients, id: \.self) { tag in

                    Text(tag).id(UUID().uuidString) // this could fix things if not unique

                }

            }

        }

    }
```