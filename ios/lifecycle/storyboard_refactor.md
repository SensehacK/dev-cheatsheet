# StoryBoard

## All things Storyboard



## References Refactor

One thing I noticed with Storyboard Refactoring, is references on storyboard with Xcode is a pain in the butt.

I spent about 30 mins on Xcode while having a video call with my parents about why it crashes on specific Segue calls and it doesn’t on specified calls.

Turns out I was doing wrong initialization across the code. As many tutorials suggested to utilize their just 1 storyboard while implementing different UIKit delegate / viewController patterns. They always used to instantiate the storyboard using “main” keyword and then instantiating those other child storyboards or view controllers.

Me being me and a bit rusty with swift development, I couldn’t fathom the Xcode error thrown in the console as Stack overflow post suggested that Xcode in latest build does some finicky stuff like always & solution to it would be “Clean build”.

I was so adamant on blaming the Xcode that I forgot the core principles of how instancing initialization works and basic error thrown meaning comprehension.

Thankfully I got my mistake which was initializing my object with “Main” and then calling other ViewControllers which aren’t even present in those.

As I had storyboard refactored and they are stored as their separate storyboard names WelcomeScreen.storyboard WelcomeScreenViewController.swift

So my initializing code should have been

```swift
let storyB = UIStoryboard(name: "WelcomeScreen", bundle: nil)
let vc1 = storyB.instantiateViewController(withIdentifier: "FirstOnboardingVC")
let vc2 = storyB.instantiateViewController(withIdentifier: "SecondOnboardingVC")
```

In which we create storyB as an UIStoryboard object. We then try to invoke instance methods of storyB with child view controllers of “WelcomeScreen” storyboard which are

* “FirstOnboardingVC"
* "SecondOnboardingVC"



## Error with Main Storyboard

```error
Failed to instantiate the default view controller for UIMainStoryboardFile 'AnotherMain' - perhaps the designated entry point is not set?
```
Just set my new `AnotherMain.storyboard` name in `Info.plist` as well as in Xcode inspector I forgot to make sure that `IsInitial View controller ` property was set.

https://stackoverflow.com/questions/20875823/failed-to-instantiate-the-default-view-controller-for-uimainstoryboardfile-main


## IB outlet errors

```error
IBoutlet is nil even when connected with storyboard

Thread 1: Fatal error: Unexpectedly found nil while implicitly unwrapping an Optional value
```
.

So my solution was I deleted the storyboard and tried invoking the ViewController programmatically but View Controller had IBOutlets connected to `Main.storyboard` so they weren't initialized as I had deleted its reference from UIKit `build setting` Xcode 14 and `Info.plist` dictionary.

Fun problem. 2 different storyboards and 2 diff ViewControllers and then programatic UI. But saving restore point to quickly discard local changes using git was really needed here. But I wasn't actively staging or commiting my changeset. Here we are. Of course this was just a practice test of combine with storyboard UI kit so no loss here.

https://stackoverflow.com/questions/29321383/iboutlet-is-nil-but-it-is-connected-in-storyboard-swift

https://www.hackingwithswift.com/example-code/uikit/how-to-fix-the-error-failed-to-instantiate-the-default-view-controller-for-uimainstoryboardfile