# UIView

## Identify UIView Uniquely

Identify uniquely which UIView is in the reference and utilize accessibility identifier to get its values.

[Uniquely identifying views](https://theswiftdev.com/uniquely-identifying-views/)

[hacking With swift](https://www.hackingwithswift.com/example-code/uikit/how-to-find-a-uiview-subview-using-viewwithtag)

## Invoke UIViewController

Init\(\) the custom UIView controller by defining the function

```swift
// MARK: - Inits
    init(isPushed: Bool) {
        self.isDisplayed = isDisplayed
        super.init(nibName: nil, bundle: nil)
    }
```

Error

```text
'required' initializer 'init(coder:)' must be provided by subclass of 'UIViewController'
```

You can avoid this by initializing the init\(coder:\)

```swift
required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
```

[cocoacasts | what-is-fatalerror-in-swift-and-when-to-use-it](https://cocoacasts.com/what-is-fatalerror-in-swift-and-when-to-use-it)


Wrapping multiple views in a sequence and executing them individually to eliminate multiple layout code and boilerplate fluff.

```swift
[customView1, customView2, customView3].forEach({
	$0.translatesAutoresizingMaskIntoConstraints = false
	$0.layer.cornerRadius = 40
	addSubview($0)
})
```

## Remove UIView

Remove the child view from superview by this command.
> view_object_name.removeFromSuperview()

Programmatic collection of UIViews

```swift
var allocatedViews: [UIView] = [UIView]()

// Programmatic adding UIViews 
for i in 0..<n {
	let childView = UIView()
	self.view.addSubview(childView)
	allocatedViews.append(childView)
}


// Programmatic deallocating UIViews
for view in allocatedViews {
    view.removeFromSuperview()
}
```
[SO](https://stackoverflow.com/questions/26569159/remove-programmatically-added-uiimageview)

[Article](http://swiftdeveloperblog.com/add-subview-and-remove-subview-example-in-swift/)



## Custom Parameters

You can utilize UIView(autoLayout = true)

```swift
private lazy var customView = UIView(useAutoLayout: true)
```

This will help us to remove the horrendous long variable setup with every override func viewDidLoad()
```swift
customView.translatesAutoresizingMaskIntoConstraints = false
```
Or you can resort to Property Wrapper of which sets these values to false.
[property_wrapper Extension AutoLayout](property_wrapper.md)

## Changes

iOS 13 changes
[SO | modal in iOS 13 fullscreen](https://stackoverflow.com/questions/56435510/presenting-modal-in-ios-13-fullscreen)

## Alpha


UIView Alpha vs UIView Subview alpha.
Alpha is the property which can basically alter a UI presentation to have full opaque visibility or have transparent visibility. So the view behind the foremost UIView gets displayed to have a hint that the UI is still present in the back of that UIView instance or UIWindow.

[SO | uiview-alpha-vs-uicolor-alpha](https://stackoverflow.com/questions/20423390/uiview-alpha-vs-uicolor-alpha)


## References

[medium | custom-uiview-in-swift-done-right](https://medium.com/@tapkain/custom-uiview-in-swift-done-right-ddfe2c3080a)

[guide-to-creating-custom-uiview](https://samwize.com/2017/11/01/guide-to-creating-custom-uiview/)
