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

> private lazy var customView = UIView(useAutoLayout: true)

This will help us to remove the horrendous long variable setup with every override func viewDidLoad()
> customView.translatesAutoresizingMaskIntoConstraints = false


## Changes

iOS 13 changes
[SO](https://stackoverflow.com/questions/56435510/presenting-modal-in-ios-13-fullscreen)

## Alpha


UIView Alpha vs UIView Subview alpha.
Alpha is the property which can basically alter a UI presentation to have full opaque visibility or have transparent visibility. So the view behind the foremost UIView gets displayed to have a hint that the UI is still present in the back of that UIView instance or UIWindow.

https://stackoverflow.com/questions/20423390/uiview-alpha-vs-uicolor-alpha