# Navigation Controller
## Navigation Stack

To check for which UINavigation ViewController is holding or presenting to present alerts sometimes we need to verify whether it internally is been hold by the UINavigationStack or parent-child relationships.


```swift
if let vc = presentingViewController.presentingViewController {
	vc.present(alertViewController, animated: true)
} 
else {
	presentingViewController.present(alertViewController,
	animated: true)
}
```


## iOS 15

Need to use UINavigationBarAppearance for updating the UINavigation Bar properties.

Before iOS 15

```swift
private let navigationController: UINavigationController = {

	let navigationController = UINavigationController()
	let navigationBar = navigationController.navigationBar
	
	navigationBar.backgroundColor = UIColor(red: 0.93, green: 0.22, blue: 0.28, alpha: 1.00)
	appearance.titleTextAttributes = [
		NSAttributedString.Key.font: UIFont(name: "Avenir-Medium", size: 32.0)!,
		NSAttributedString.Key.foregroundColor: UIColor.white
	]
	
	return navigationController
}()

```

After iOS 15
```swift
private let navigationController: UINavigationController = {

	let navigationController = UINavigationController()
	let navigationBar = navigationController.navigationBar
	let appearance = UINavigationBarAppearance()
	
	appearance.configureWithOpaqueBackground()
	appearance.backgroundColor = UIColor(red: 0.93, green: 0.22, blue: 0.28, alpha: 1.00)
	appearance.titleTextAttributes = [
		NSAttributedString.Key.font: UIFont(name: "Avenir-Medium", size: 32.0)!,
		NSAttributedString.Key.foregroundColor: UIColor.white
	]
	
	navigationBar.standardAppearance = appearance;
	navigationBar.scrollEdgeAppearance = navigationBar.standardAppearance	
	
	return navigationController
}()
```

[Apple Dev forums](https://developer.apple.com/forums/thread/682420)

`isTranslucent` property being added in iOS 13 which has different behavior with UI NavigationBar background color.
https://sarunw.com/posts/uinavigationbar-changes-in-ios13/

## Text Attributes not updating

You need to update the property using UINavigationBarAppearance or else it won't work with whatever text attribute being set towards the title.

```swift
//This is the line that doesnt work :( 
navigationBar.titleTextAttributes = [NSAttributedString.Key.foregroundColor: UIColor.white
```

You can use object of  `UINavigationBarAppearance` & update the code. It could also depend on whether you're using `preferLargeTitle` property on navigation bar.

```swift

let appearance = UINavigationBarAppearance()
appearance.titleTextAttributes = [

	NSAttributedString.Key.font: UIFont(name: "Avenir-Medium", size: 32.0)!,

	NSAttributedString.Key.foregroundColor: UIColor.white

]
```

[SO](https://stackoverflow.com/questions/54207002/uinavigationbar-wont-set-title-text-attributes)


## Theming UIBarButtons

As my fellow [media fanatic mentor](README###Mentors IRL) helped me once with the UINavigationBar or whatever apple UIKit framework has renamed it to now.
We need to set the parent Viewcontroller navigation property rather than changing the child UI ViewController class.
It makes sense but yes the documentation or my understanding of documentation could have been better.


```swift
let backItem = UIBarButtonItem(title: "Back", style: .plain, target: nil, action: nil)
backItem.tintColor = UIColor.red
navigationItem.backBarButtonItem = backItem
```

Here is his snippet of Gitlab Merge Request Code review comment.

```markdown

this is the proper way to theme the back button that's visible sun the nav bar when viewing the `FieldMetaType ListViewController`.

it seems odd that a change in a different file would be the fix, but back bar button items are usually owned by the view controller that's below the currently visible view controller in a navigation controller. this actually makes sense tho when you consider that the back button's content is actually driven by the previous view controller's content.

we're only showing the back button, but if there was a back button title, we would want it to be set by the view controller that already knows title. and that's exactly what `UINavigationItem` does for us, allows us to configure everything related to this view controller's navigation bar content and behavior (which is only used if this view controller is used inside of a `UINavigationController`).

even though `UINavigationItem` itself doesn't represent a distinct UI component, it's an abstraction that is used within the specific context of push/pop style navigation.
```


https://stackoverflow.com/questions/28733936/change-color-of-back-button-in-navigation-bar

https://www.youtube.com/watch?v=7KdRpFEOG9I


## Navigation Items


[SO](https://stackoverflow.com/questions/39643169/swift-hide-navigation-title-but-show-its-title-as-back-button-in-next-view-contr)

Try to hide titleView label

```swift
self.navigationItem.titleView = UIView()
```


## Quirks

### Navigation bar
Large title text navigation
[SO](https://stackoverflow.com/questions/47649375/ios-11-large-navigation-bar-title-unexpected-velocity)

[navigation bar glitches](https://swiftsenpai.com/development/large-title-uinavigationbar-glitches/)

https://stackoverflow.com/questions/69111478/ios-15-navigation-bar-transparent


## Swap ViewController

Swap or Replace View Controllers.

```swift
extension UINavigationController {
    func swap(currentViewController: UIViewController,
              newViewController: UIViewController,
              animated: Bool = false) {
        var controllerStack = self.viewControllers
        if let index = controllerStack.firstIndex(of: currentViewController) {
            controllerStack[index] = newViewController
        }
        setViewControllers(controllerStack, animated: animated)
    }
```

## Pop View Controllers

https://stackoverflow.com/questions/26132658/pop-2-view-controllers-in-nav-controller-in-swift

https://developer.apple.com/forums/thread/134078
## References

https://dmtopolog.com/navigation-bar-customization/