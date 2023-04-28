# View Controllers

## Creation

Different types of View controller can be utilized. We would initialize view controller using storyboard and setting the controller in the inspector.

The parent view will perform a segue and call upon the storyboard using Storyboard references and storyboard name.

## Present

This would be better explained using iOS Segues doc as we would dive more deep into that doc about creating segues and linking them differently.

## Dismiss

Dismissing Child view controller could be done using various methods depending on how it was created.

View Controller: 

> Normal View controller uses just dismiss method. self.dismiss\(animated: true, completion: nil\)

Navigation Controller: 

> navigationController?.dismiss\(animated: true\)


## Pop

Navigation controller needs pop method to pop the current view controller into the navigation stack


> navigationController?.popViewController\(animated: true\)

[SO](https://stackoverflow.com/questions/23841617/how-to-pop-navigation-controller-ios)

We can also dismiss the the whole 


## Presentation iOS 13
Different styles [Medium article](https://hacknicity.medium.com/view-controller-presentation-changes-in-ios-13-ac8c901ebc4e)

## Init


```swift
required init?(coder aDecoder: NSCoder) {
    super.init(coder: aDecoder)
}
```

---
https://stackoverflow.com/questions/24036393/fatal-error-use-of-unimplemented-initializer-initcoder-for-class


## Container Child View

[uiview](uiview.md)

https://cocoacasts.com/managing-view-controllers-with-container-view-controllers/

https://guides.codepath.com/ios/Adding-and-Removing-Child-View-Controllers


## No Storyboard Xcode

No `main.storyboard` in new project
Basically remove its references and just create a new ViewController() instance and set its view to rootView

Depending on whether your app uses `AppDelegate` or `SceneDelegate` 

AppDelegate

```swift
var window: UIWindow?

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {    
	let window = UIWindow(frame: UIScreen.main.bounds) 
	window.rootViewController = ViewController()    
	window.makeKeyAndVisible()
	self.window = window										
	return true											
}
```

SceneDelegate

```swift
func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {    

	guard let windowScene = (scene as? UIWindowScene) else { return }
    let window = UIWindow(windowScene: windowScene)    window.rootViewController = ViewController()
    window.makeKeyAndVisible()
    self.window = window
}
```


https://sarunw.com/posts/how-to-create-new-xcode-project-without-storyboard/



## Errors

Warning: Attempt to present * on *whose view is not in the window hierarchy"



This could be because there is timing issue when presenting the view controller.
So it is safe to do this after some event has happened via a button or a delay.

```swift
override func viewDidAppear(_ animated: Bool) {
        initializeAnotherView()
}
```

But to be extra sure you can present another screen after the ViewLifecycle method named `viewDidAppear()` is called and then try to present that view controller.



## Resources

[Custom Presentation Controllers](https://makeapppie.com/2016/04/11/the-step-by-step-guide-to-custom-presentation-controllers/)

[Diff ViewControllers](https://stackoverflow.com/questions/33395463/in-uinavigationcontroller-what-is-the-difference-between-topviewcontroller-visi)

[Basic Presentation Controllers](https://www.appcoda.com/presentation-controllers-tutorial/)

[Apple docs archive](https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/PresentingaViewController.html)