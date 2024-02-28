
Table equivalent of UIKit in swiftUI


```swift
List(viewModel.pokemons, id: \.id) { pokemon in

}

```


## Grids

Recently introduced in iOS 16.
More robust and available easily.

## Detect Taps

Use  `onTapGesture`
```swift
.onTapGesture {
    print("Tapped cell")  // This triggers when you tap anywhere in the cell
}
```

or use a button wrapped inside the view

```swift
VStack {
    Button(action: {
        print("Tapped")
    }) {
        Text("Hello world")
    }
}
```

[SO | detect taps on a List cell row in SwiftUI](https://stackoverflow.com/questions/68346592/how-to-detect-taps-on-a-list-cell-row-in-swiftui)


## References

[swiftui labs | impossible-grids](https://swiftui-lab.com/impossible-grids/)

[sarunw | swiftui-grid](https://sarunw.com/posts/swiftui-grid/)








