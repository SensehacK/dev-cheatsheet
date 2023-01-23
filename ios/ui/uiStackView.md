# UI StackView



## Implementation


## Programmatically

[SO](https://stackoverflow.com/questions/30728062/add-views-in-uistackview-programmatically)

## Article

[Hidden gems of UIStackView](https://medium.com/dolap-tech/hidden-gems-of-uistackview-3b94a0001d29)

[Distribution Types](https://www.hackingwithswift.com/example-code/uikit/what-are-the-different-uistackview-distribution-types)

[Animating subview](https://www.hackingwithswift.com/read/33/3/animating-uistackview-subview-layout)

[Custom UI Elements on StackView](https://exploringswift.com/blog/using-uistackview-custom-uibutton-class-to-add-buttons-to-twittercard-interface-part-2)

## Documentation

[Apple Developer](https://developer.apple.com/documentation/uikit/uistackview)




## Debug

Errors: 

```libc++abi.dylib: terminating with uncaught exception of type NSException
*** Terminating app due to uncaught exception 'NSGenericException', reason: 'Unable to activate constraint with anchors <NSLayoutXAxisAnchor:0x600001575e00 "UIButton:0x7fafea124c50.centerX"> and <NSLayoutXAxisAnchor:0x600001570980 "UIView:0x7fafdffa97f0.centerX"> because they have no common ancestor.  Does the constraint or its anchors reference items in different view hierarchies?  That's illegal.'
terminating with uncaught exception of type NSException
```

Constraint common view hierarchy error.




## UIView Events

If you're embeding UIstackView in a UIView class and are not able to get some event responses, you need disable its user interaction flag.

```swift
class CustomView: UIButton {
	init() {
        super.init(frame: .zero)
		labelStackView.addArrangedSubviews(titleStackView, descriptionLabel)
        addSubview(labelStackView)
    }
    
	private(set) var labelStackView: UIStackView = {
		stackView.isUserInteractionEnabled = false
	}
```