

### Dismiss View

```swift 
@Environment(\.dismiss) var dismiss

// Call to dismiss
dismiss()

```

https://stackoverflow.com/a/72885925/5177704



## Error

```
“Function declares an opaque return type, but has no return statements in its body from which to infer an underlying type”
```

I was able to fix it by having to explicitly mention 
`return NavigationView { }` after I tacked on `.onAppear{ performAnotherTask() }` calling another external function in the same view struct.

https://www.hackingwithswift.com/quick-start/swiftui/how-to-fix-function-declares-an-opaque-return-type-but-has-no-return-statements-in-its-body-from-which-to-infer-an-underlying-ty