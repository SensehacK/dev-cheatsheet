NavigationController



## Quirks

### Navigation bar
Large title text navigation
[SO](https://stackoverflow.com/questions/47649375/ios-11-large-navigation-bar-title-unexpected-velocity)

[navigation bar glitches](https://swiftsenpai.com/development/large-title-uinavigationbar-glitches/)


## Navigation Stack


To check for which UINavigation ViewController is holding or presenting to present alerts sometimes we need to verify whether it internally is been hold by the UINavigationStack or parent-child relationships.


```swift

if let vc = presentingViewController.presentingViewController {
		vc.present(alertViewController, animated: true)
} 
else {
		presentingViewController.present(alertViewController, animated: true)
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

References

https://dmtopolog.com/navigation-bar-customization/