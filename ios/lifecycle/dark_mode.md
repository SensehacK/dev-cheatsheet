# Dark Mode



## Checking User Style

```swift
switch UIScreen.main.traitCollection.userInterfaceStyle { 
	case .light: //light mode 
	case .dark: //dark mode 
	case .unspecified: //the user interface style is not specified
}
```

## Override the App user style

You could use User Defaults to save the in app settings for different themes.

## Xcode assets

Utilize Color Set in Xcode with “Any” & “Dark” Mode. To better update the application with dynamic settings.



## Dynamic colors

https://www.swiftbysundell.com/articles/defining-dynamic-colors-in-swift/


## Detect UI Appearance Change


```swift
override func traitCollectionDidChange(_ previousTraitCollection: UITraitCollection?) {
    super.traitCollectionDidChange(previousTraitCollection)

    if traitCollection.hasDifferentColorAppearance(comparedTo: previousTraitCollection) {
        callCustomFunc()
    }
}
```

https://stackoverflow.com/questions/58312095/ios13-dark-mode-change-not-recognized-by-tableview-cell

https://stackoverflow.com/questions/58016866/how-to-detect-light-dark-mode-change-in-ios-13


## Single View Override

[First retrieve color scheme of the app.](ios/swiftUI/environment#Retrieving)

### SwiftUI
Specific single view passed with environment or 
```swift
.environment(\.colorScheme, .light) // or .dark
// OR
.preferredColorScheme(.dark)
```


## Entire App Color scheme
### UIKit 

Each `UIView` has access to the window, So you can use it to set the `. overrideUserInterfaceStyle` value to any scheme you need.

```swift
myView.window?.overrideUserInterfaceStyle = .dark
```

### SwiftUI 




Copied from [StackOverflow post](https://stackoverflow.com/questions/58476048/implement-dark-mode-switch-in-swiftui-app) 

First you need to access the window to change the app colorScheme that called `UserInterfaceStyle` in `UIKit`.

I used this in `SceneDelegate`:

```swift
private(set) static var shared: SceneDelegate?

func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
    Self.shared = self
    ...
}
```

Then you need to bind an action to the toggle. So you need a model for it.

```swift
struct ToggleModel {
    var isDark: Bool = true {
        didSet { 
            SceneDelegate.shared?.window!.overrideUserInterfaceStyle = isDark ? .dark : .light 
        }
    }
}
```

At last, you just need to toggle the switch:

```swift
struct ContentView: View {
     @State var model = ToggleModel()

     var body: some View {
         Toggle(isOn: $model.isDark) {
             Text("is Dark")
        }
    }
}
```



## Resources

Full guide: 

https://www.avanderlee.com/swift/dark-mode-support-ios/

Material Design

https://m2.material.io/design/color/dark-theme.html#usage

Disable Dark mode
https://sarunw.com/posts/how-to-disable-dark-mode-in-ios/

Supporting dark mode
https://medium.com/@iAkashlal/enabling-dark-mode-support-for-your-ios-applications-cd98d79033de

https://developer.apple.com/documentation/uikit/appearance_customization/supporting_dark_mode_in_your_interface

https://www.kodeco.com/10718147-supporting-dark-mode-adapting-your-app-to-support-dark-mode

https://letcreateanapp.com/2021/08/08/adding-support-of-dark-mode-in-ios-app-in-swift/
## Tools

https://www.uicolor.io/

https://www.canva.com/colors/color-wheel/
Use `Monochromatic` when working with Black - White Mono colors
And use `Complementary` mode when working with RGB colors

Thanks to Design team Member
Contrast checker
https://webaim.org/resources/contrastchecker/

Figma plugin 
https://www.figma.com/community/plugin/748533339900865323