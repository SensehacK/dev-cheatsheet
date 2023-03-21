
## Intro

Adding VC as a scrollable VCs to swipe as the onboarding flow in iOS.


## Usage




## Overriden Methods Calls

UIKit lifecycle methods being subscribed.
In order to have this method be intercepted  by UIKit -> UIViewController when you have overridden methods such as `ViewWillTransition` . You need to first add the content view controllers to the ViewController hierarchy. 

```swift 
override func viewWillTransition(to size: CGSize, with coordinator: UIViewControllerTransitionCoordinator) { }
```

By using `.addChild()` method you would append the UIViewControllers to the view controller hierarchy - UIKit parsing overriden methods irrespective of the child views being rendered or not.

My teammates comment about the it 

```text
so configuring the page controller with the view controllers that it’s in charge of displaying add the content view controllers to the hierarchy. but we weren’t adding the page controller (itself a view controller container) to the view controller hierarchy, only its view to the view hierarchy. so adding the page controller to the view controller hierarchy automatically added all of it’s children to the view controller hierarchy.it’s exactly like appending an isolated tree as a subtree to a large tree.
```




## NS Internal InconsistencyException

```error
pageViewController setViewControllers crashes with "Invalid parameter not satisfying: [views count] == 3
```

This happens only when the code block isn't being called upon from Main thread or higher `.qos` for asynchronous code path execution.

https://stackoverflow.com/questions/24000712/pageviewcontroller-setviewcontrollers-crashes-with-invalid-parameter-not-satisf

The solution according to the Stack Overflow thread is to make sure utilze GCD tools in order to switch the thread back to main thread for UI work.
dispatch_async on the main queue

```objC
dispatch_async(dispatch_get_main_queue(), ^ {  });
```

```swift
DispatchQueue.main.async { 
	self.pageViewController?.setViewControllers()
}
```


## Resources

https://www.youtube.com/watch?v=hIMRn_LdvOg