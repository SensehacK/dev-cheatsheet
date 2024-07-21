
## Intro

Grid layout could be described kinda a like a horizontal and vertical spacers with content in them.


## Code



```swift
let layout = [
    GridItem(.adaptive(minimum: 80, maximum: 120)),
]

ScrollView(.horizontal) {
    LazyHGrid(rows: layout) {
        ForEach(0..<1000) {
            Text("Item \($0)")
        }
    }
}

```


## References

[HWS | how-to-lay-out-views-in-a-scrolling-grid](https://www.hackingwithswift.com/books/ios-swiftui/how-to-lay-out-views-in-a-scrolling-grid)
