

### Dismiss View

```swift 
@Environment(\.dismiss) var dismiss

// Call to dismiss
dismiss()

```

https://stackoverflow.com/a/72885925/5177704



Importance of Spacer

https://medium.com/geekculture/understanding-spacers-and-padding-in-swift-ui-e1fb5f6efa44

https://www.hackingwithswift.com/quick-start/swiftui/how-to-control-spacing-around-individual-views-using-padding
## MaxWidth


https://designcode.io/swiftui-handbook-max-width-and-frame-alignment

https://stackoverflow.com/questions/57345136/how-to-make-a-view-max-width-with-padding-in-swiftui


## Safe Area


https://www.hackingwithswift.com/quick-start/swiftui/how-to-inset-the-safe-area-with-custom-content


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

https://www.hackingwithswift.com/quick-start/swiftui/how-to-fix-function-declares-an-opaque-return-type-but-has-no-return-statements-in-its-body-from-which-to-infer-an-underlying-ty


## UIKit Interop

```swift
let swiftView = UIHostingController(rootView: SwiftUIView())

present(swiftView, animated: true)

```

https://sarunw.com/posts/swiftui-in-uikit/

https://sarunw.com/posts/swiftui-view-as-uiview/

https://sarunw.com/posts/swiftui-view-as-uiviewcontroller/