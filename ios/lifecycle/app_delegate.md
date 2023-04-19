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


## Swift UI App State Reactive

```swift
struct ContentView: View {
    @Environment(\.scenePhase) var scenePhase

    var body: some View {
        Text("Hello, world!")
            .padding()
            .onChange(of: scenePhase) { newPhase in
                if newPhase == .active {
                    print("Active")
                } else if newPhase == .inactive {
                    print("Inactive")
                } else if newPhase == .background {
                    print("Background")
                }
            }
    }
}
```

https://www.hackingwithswift.com/books/ios-swiftui/how-to-be-notified-when-your-swiftui-app-moves-to-the-background


## Initial ViewController called Twice

Turns out when removing my Storyboard reference and replacing that logic in `AppDelegate` as well as `Scene Delegate` . I was invoking my `ViewController` from both places.
So with iOS 16 my current simulator. Scene Delegate Life cycle was calling my view controller first and then `AppDelegate` was also calling my View again. 
Removing the AppDelegate `UIWindow` object initialization removed the `viewDidLoad` getting called twice.


Maybe relevant SO I didn't find a solution from the accepted one but still including it.
https://stackoverflow.com/questions/1081131/viewdidload-getting-called-twice-on-rootviewcontroller-at-launch

https://stackoverflow.com/questions/7079602/viewdidload-is-called-twice