
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


Use `contentShape` to get full tappable area option and you may also need to add `Spacer()` in between List Cell `HStack | VStack` component in order to get the whole cell from left / right accessory view to be tappable.  Since by default SwiftUI isn't fully tappable on instances.

```swift
.contentShape(Rectangle())
```

[HWS | source](https://www.hackingwithswift.com/quick-start/swiftui/how-to-control-the-tappable-area-of-a-view-using-contentshape)



## Performance


[List vs lazyVstack deep dive](https://fatbobman.com/en/posts/list-or-lazyvstack)

## References

[swiftui labs | impossible-grids](https://swiftui-lab.com/impossible-grids/)

[sarunw | swiftui-grid](https://sarunw.com/posts/swiftui-grid/)








