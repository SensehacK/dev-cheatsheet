# Orientation




## App Delegate

You can customize it depending on runtime for loading the app in specific portrait state and then supporting or unlocking it to all orientations.
The info.plist has independent orientation support for iPhone and iPad which can be also edited in Targets "Main.app" -> General Tab under "Deployment Info"

## Implementation

You can override it on any UIView controller.

```swift
var supportedOrientations: UIInterfaceOrientationMask {
        return CurrentDevice.isiPhone ? .portrait : .all
    }
```

UIInterfaceOrientationMask supports an enum with different orientation locks.


[Rotating iPhones](https://useyourloaf.com/blog/upside-down-and-rotating-iphones/)



## Global App Delegate Implementation


[Source SO](https://stackoverflow.com/questions/28938660/how-to-lock-orientation-of-one-view-controller-to-portrait-mode-only-in-swift/41811798#41811798)

Things can get quite messy when you have a complicated view hierarchy, like having multiple navigation controllers and/or tab view controllers.

This implementation puts it on the individual view controllers to set when they would like to lock orientations, instead of relying on the App Delegate to find them by iterating through subviews.

Swift 3, 4, 5

In AppDelegate:

/// set orientations you want to be allowed in this property by default
var orientationLock = UIInterfaceOrientationMask.all

func application(_ application: UIApplication, supportedInterfaceOrientationsFor window: UIWindow?) -> UIInterfaceOrientationMask {
        return self.orientationLock
}

In some other global struct or helper class, here I created AppUtility:

struct AppUtility {

    static func lockOrientation(_ orientation: UIInterfaceOrientationMask) {
    
        if let delegate = UIApplication.shared.delegate as? AppDelegate {
            delegate.orientationLock = orientation
        }
    }

    /// OPTIONAL Added method to adjust lock and rotate to the desired orientation
    static func lockOrientation(_ orientation: UIInterfaceOrientationMask, andRotateTo rotateOrientation:UIInterfaceOrientation) {
   
        self.lockOrientation(orientation)
    
        UIDevice.current.setValue(rotateOrientation.rawValue, forKey: "orientation")
        UINavigationController.attemptRotationToDeviceOrientation()
    }

}

Then in the desired ViewController you want to lock orientations:

 override func viewWillAppear(_ animated: Bool) {
    super.viewWillAppear(animated)
    
    AppUtility.lockOrientation(.portrait)
    // Or to rotate and lock
    // AppUtility.lockOrientation(.portrait, andRotateTo: .portrait)
    
}

override func viewWillDisappear(_ animated: Bool) {
    super.viewWillDisappear(animated)
    
    // Don't forget to reset when view is being removed
    AppUtility.lockOrientation(.all)
}

If iPad or Universal App

Make sure that "Requires full screen" is checked in Target Settings -> General -> Deployment Info. supportedInterfaceOrientationsFor delegate will not get called if that is not checked.


```swift
// App Utility for universal app tweaking
struct AppUtility {
    
    enum Orientation {
        case portrait
        case all
    }

static func setLockOrientation(_ orientation: Orientation) {
        
        switch orientation {
        case .portrait:
            if Device.isHandset { lockOrientation(.portrait, andRotateTo: .portrait) }
            
        case .all:
            if Device.isHandset {
                lockOrientation(.all,
                                andRotateTo: UIInterfaceOrientation(rawValue: UIDevice.current.orientation.rawValue) ?? .portrait) }
        }
        
    }
}
```

[HWS](https://www.hackingwithswift.com/example-code/uikit/how-to-read-the-interface-orientation-portrait-or-landscape)

To detect current orientation you could check it in 

> UIDevice.current.orientation 
// returns enum value or can extract its .rawvalue as well

```
// To set orientation 
UIDevice.current.setValue(rotateOrientation.rawValue, forKey: "orientation")

// To rotate to the set current orientation
UINavigationController.attemptRotationToDeviceOrientation()
```


## viewWillLayoutSubviews

You need to call the layout code again to properly align the UI view frame bounds.

The sublayers are not automatically resized to fit the view: you should update them when the view gets its layout pass:

```swift
func viewWillLayoutSubviews() { }
```

https://stackoverflow.com/questions/38358081/gradient-layer-is-not-working-on-landscape-mode-swift

https://stackoverflow.com/questions/23457391/when-are-the-viewwilllayoutsubviews-and-viewdidlayoutsubviews-methods-called

https://stackoverflow.com/questions/20995336/why-does-uiviewcontroller-almost-always-require-layoutsubviews