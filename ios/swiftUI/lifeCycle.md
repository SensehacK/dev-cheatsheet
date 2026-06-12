

## App View Lifecycle


Life cycle methods in Swift UI
[view-life-cycle-methods-in-swiftui](https://betterprogramming.pub/view-life-cycle-methods-in-swiftui-b7fa9f0e8dfb)


onAppear and onDisappear methods
[HWS | how-to-respond-to-view-lifecycle-events-onappear-and-ondisappear](https://www.hackingwithswift.com/quick-start/swiftui/how-to-respond-to-view-lifecycle-events-onappear-and-ondisappear)



## Scene Lifecycle


- Active scenes are running right now, which on iOS means they are visible to the user. On macOS an app’s window might be wholly hidden by another app’s window, but that’s okay – it’s still considered to be active.
- Inactive scenes are running and might be visible to the user, but the user isn’t able to access them. For example, if you’re swiping down to partially reveal the control center then the app underneath is considered inactive.
- Background scenes are not visible to the user, which on iOS means they might be terminated at some point in the future.

```swift
struct ContentView: View {
    @Environment(\.scenePhase) var scenePhase

    var body: some View {
        Text("Hello, world!")
            .onChange(of: scenePhase) { oldPhase, newPhase in
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

[HWS | scenePhase SwiftUI](https://www.hackingwithswift.com/books/ios-swiftui/how-to-be-notified-when-your-swiftui-app-moves-to-the-background)
