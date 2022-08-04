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
