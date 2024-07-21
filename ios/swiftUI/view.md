

### Dismiss View

```swift 
@Environment(\.dismiss) var dismiss

// Call to dismiss
dismiss()

```
[SO | dismiss](https://stackoverflow.com/a/72885925/5177704)


Importance of Spacer
[understanding-spacers-and-padding-in-swift-ui](https://medium.com/geekculture/understanding-spacers-and-padding-in-swift-ui-e1fb5f6efa44)

[HWS | how-to-control-spacing-around-individual-views-using-padding](https://www.hackingwithswift.com/quick-start/swiftui/how-to-control-spacing-around-individual-views-using-padding)

## MaxWidth

[swiftui-handbook-max-width-and-frame-alignment](https://designcode.io/swiftui-handbook-max-width-and-frame-alignment)


[SO | how-to-make-a-view-max-width-with-padding-in-swiftui](https://stackoverflow.com/questions/57345136/how-to-make-a-view-max-width-with-padding-in-swiftui)

## Safe Area

[HWS | how-to-inset-the-safe-area-with-custom-content](https://www.hackingwithswift.com/quick-start/swiftui/how-to-inset-the-safe-area-with-custom-content)



## Some View

You need a function to make return statements `-> some view`

In this function you can't have guard let statements since that paired with `AsyncImage -> AsyncImagePhase enum` could confuse the compiler about the type of data being returned. It couldn't infer properly. 

You need to make sure that whatever return type you're sending conforms to both return type.

## Error

```
“Function declares an opaque return type, but has no return statements in its body from which to infer an underlying type”
```

I was able to fix it by having to explicitly mention 
`return NavigationView { }` after I tacked on `.onAppear{ performAnotherTask() }` calling another external function in the same view struct.

[HWS | how-to-fix-function-declares-an-opaque-return-type-but-has-no-return-statements-in-its-body-from-which-to-infer-an-underlying-ty](https://www.hackingwithswift.com/quick-start/swiftui/how-to-fix-function-declares-an-opaque-return-type-but-has-no-return-statements-in-its-body-from-which-to-infer-an-underlying-ty)



## UIKit Interop

```swift
let swiftView = UIHostingController(rootView: SwiftUIView())

present(swiftView, animated: true)

```
[sarunw | swiftui-in-uikit](https://sarunw.com/posts/swiftui-in-uikit/)

[sarunw | swiftui-view-as-uiview](https://sarunw.com/posts/swiftui-view-as-uiview/)

[sarunw | swiftui-view-as-uiviewcontroller](https://sarunw.com/posts/swiftui-view-as-uiviewcontroller/)


## Refactor Massive SwiftUI Views

[three-ways-to-refactor-massive-swiftui-views](https://holyswift.app/three-ways-to-refactor-massive-swiftui-views/)




## Warnings

**Invalid frame dimension (negative or non-finite)**.
Code 
```swift
.frame(maxWidth: .infinity, maxHeight: 150)
```

[Source](https://www.hackingwithswift.com/forums/100-days-of-swiftui/invalid-frame-dimension/15353)
// Text script
The error message proved to be stale, remaining from the time when the code was written like
```swift
.frame(width: .infinity, height: 150)
```

After re-building the code, the warnings disappeared.
// Text end

So I'm guessing is the frame needs to provide min / max Width or Height. Having just `width` set to `.infinity` is what makes it have that invalid frame dimension. Since width can't be just directly set to non-infinite value. MaxWidth could be set to `.infinity` provided that `minWidth` will just try to make it work with the window or UIScreen view bounds.




## Preview not working

Closing tabs worked for me but it seems I mixed up iPad & VisionOS which has realityPro Kit package which is only available for VisionOS. So it was a bit harder to remove that dependency to build it for iPadOS

[SO | swiftui-canvas-content-view-previews-not-found-in-any-targets](https://stackoverflow.com/questions/65384298/xcode-swiftui-canvas-content-view-previews-not-found-in-any-targets)


## print in swiftUI

You can use print statements inside views like this:

```swift
VStack(alignment: .leading) {
    if workoutManager.averageHeartRate < roundedKarvonenValue {
        let _ = print(itemX.randomElement()!)
    } else {
        let _ = print(itemY.randomElement()!)
    }
}
```