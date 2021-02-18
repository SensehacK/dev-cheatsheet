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

