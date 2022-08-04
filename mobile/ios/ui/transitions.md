# transitions

Transitioning from one view controller to another is always great way to show how the views or the flow of data / work is being carried out.
It can literally make or break the User Experience of the end user and also needs to be not done overly complicated with too many animations.
Looking for sweet spot is important in that aspect.


## Delegates


## Custom Transition Animation

You can always go for custom transition animation route when you're ready for it.
For Navigation Controller embedded transitions
```swift
// 1
customViewController.modalPresentationStyle = .fullScreen

// 2
let transition = CATransition()
transition.duration = 0.2
transition.timingFunction = CAMediaTimingFunction(name: .easeOut)
transition.type = .push
transition.subtype = .fromLeft

// 3
navigationController.view.window?.layer.add(transition, forKey: kCATransition)
navigationController.present(customViewController, animated: false)
})
```


For default UIViewController transitions

```swift
self?.view.window?.layer.add(transition, forKey: kCATransition)
self?.dismiss(animated: false, completion: nil)
```

**Important Note**
When using custom transitions make sure that you disable the animated bool flag by passing 'false' value when calling default UI functions.

[UIVC custom transition](https://sweettutos.com/2020/10/04/custom-transition-animation-for-uiviewcontroller-using-core-animation/) ✅ 

[Custom Transition tutorial](https://www.appcoda.com/custom-view-controller-transitions-tutorial/)

[Medium article Swift 4](https://medium.com/@ludvigeriksson/custom-interactive-uinavigationcontroller-transition-animations-in-swift-4-a4b5e0cefb1e)

[Simple navigation transition](https://medium.com/@artrmz/simple-custom-uinavigationcontroller-transitions-fdb56a217dd8)

## Sources

[IPhone_Rotation,_View_Resizing_and_Layout_Handling](https://www.techotopia.com/index.php/IPhone_Rotation,_View_Resizing_and_Layout_Handling)