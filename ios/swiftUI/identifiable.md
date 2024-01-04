# Identifiable

## Intro

`A class of types whose instances hold the value of an entity with stable identity.` - Apple Docs

## Working with Identifiable

[Hacking with Swift article](https://www.hackingwithswift.com/books/ios-swiftui/working-with-identifiable-items-in-swiftui)

```swift
let model: MealRecipeDetailViewModel
let gridItems = [GridItem(.adaptive(minimum: 60))]
var body: some View {
    VStack {
        Text(Constants.ingredients)
            .font(.headline)
        LazyVGrid(columns: gridItems, alignment: .center) {
            ForEach(model.recipeMeal.ingredients,
             id: \.self) { tag in
                Text(tag).id(UUID().uuidString) // this could fix things if not unique
            }
        }
    }
}
```
 
## Expected argument type `Range < >`

Cannot convert value of type `[array]` to expected argument type `Range<Int>`

Make the `struct customObject` conform to Identifiable

```swift
struct A: Identifiable {
    var id: String {
        return /*some ID*/
    }
}
```

## Struct vs Class

Struct when conforming to protocol identifiable will throw a compile error.
 `Type Bar does not conform to protocol Identifiable`
 
```swift
class Foo: Identifiable { }

struct Bar: Identifiable { }
```

That is because there is an explicit extension for `Identifiable`, which makes  classes to not have explicit `id` defined.

```swift
extension Identifiable where Self : AnyObject {
    /// The stable identity of the entity associated with this instance.
    public var id: ObjectIdentifier { get }
}
```
