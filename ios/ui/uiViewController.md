
## Intro

UIViewController is the basic View Controller in iOS - Swift

```swift
let vc = UIViewController()
vc.backgroundColor = .red
```



## iOS 13 ViewController Changes

New changes brought in with iOS 13 is the dismissal option for UIViewControllers being presented via `.pageSheet` & `.formSheet` 

[iOS 13 changes](https://hacknicity.medium.com/view-controller-presentation-changes-in-ios-13-ac8c901ebc4e)


### Turn off interactive dismissal

Option 1
```swift
viewController.isModalInPresentation = true
```

Option 2
```swift
func presentationControllerShouldDismiss(_ presentationController: UIPresentationController) -> Bool {
    return false
}
```

[SO](https://stackoverflow.com/questions/56459329/disable-the-interactive-dismissal-of-presented-view-controller)