# App Delegate Lifecycle





 
## Scene Delegate Migration
Swift 5 brought up with some new changes to app delegate and dividing them into 2 parts to cater it better for multiple screen sizes and iPadOS counterparts.
[Good small snippet](https://dev.to/kevinmaarek/add-a-scene-delegate-to-your-current-project-5on)


[State Lifecycle](https://www.dummies.com/web-design-development/mobile-apps/basics-of-states-in-the-lifecycle-of-an-ios-app/)



## Crash App

If for some reason you want to crash your application purposefully. You can just explicitly unwrap an optional which is guaranteed to be nil with a `bang` operator.
```swift
let optional: String? = nil
print(optional!)
```

I'm presuming we also have an option to send a SignalAlert / Interrupt to iOS Springboard to crash to home screen.


```swift
fatalError()
// OR
preconditionFailure()
```

https://stackoverflow.com/questions/32511178/easiest-way-to-force-a-crash-in-swift


## App lifecycle



`applicationDidBecomeActive` 
`applicationWillEnterForeground`


`didFinishLaunchingWithOptions`

https://medium.com/@ansujain/ios-application-life-cycle-d517a3c44e7e

[SO](https://stackoverflow.com/questions/10304780/applicationdidbecomeactive-getting-called-twice)