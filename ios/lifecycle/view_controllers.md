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

## Resources

[Custom Presentation Controllers](https://makeapppie.com/2016/04/11/the-step-by-step-guide-to-custom-presentation-controllers/)

[Diff ViewControllers](https://stackoverflow.com/questions/33395463/in-uinavigationcontroller-what-is-the-difference-between-topviewcontroller-visi)

[Basic Presentation Controllers](https://www.appcoda.com/presentation-controllers-tutorial/)

[Apple docs archive](https://developer.apple.com/library/archive/featuredarticles/ViewControllerPGforiPhoneOS/PresentingaViewController.html)