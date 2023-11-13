# Notification  Pattern

## Default

```swift
func listenObserver() {
    NotificationCenter
    .default
    .addObserver(forName: 
    Notification.Name(rawValue: notificationName),            
    object: object, 
    queue: nil, 
    using: closure)
}

func post
```

### Maintain Array of Notification Observers

```swift
class NotificationBusContainer : NSObject { 

    // Variables to manage Notification state
    private let postingQueue = DispatchQueue(label: "com.companyName.projectName.notificationBusContainer",qos: .utility)
    /// Array of Notifications
    private var observerTokens: [NSObjectProtocol]
    /// Extra class ref to be passed around in Notifications
    private var otherClassRef: CustomClass()
    /// Bubble up event / Process Events
    private var processBus = ProcessEventsBus()
    
    init () { 
        self.observerTokens = [NSObjectProtocol]()
        super.init()
    }
    
    deinit {
        postingQueue.sync {
            unhookNotifications()
        }
    }

    /// Public function for explicit notifications state reset
    @objc public func disconnect() {
        postingQueue.sync {
            unhookNotifications()
        }
    }

    /// Internal func where we remove all notification observers
    func unhookNotifications() {
        for observerToken in observerTokens { 
            NotificationCenter
            .default
            .removeObserver(observerToken)
        }
        observerTokens.removeAll()
    }

    /// Internal convenience func for adding notifications to the internal Notification array state.
    func addObserver(forName notificationName: String,
    withObject object: Any?,
    withClosure closure: @escaping (Notification) -> ()) {
        let token = NotificationCenter
        .default
        .addObserver(
            forName: Notification
                .Name(rawValue:notificationName),
            object: object,
            queue: nil,
            using: closure)
            
        observerTokens.append(token)
    }


    func addCustomNotification() {
        addObserver(forName: "KAUTILYA_CUSTOM_NS_NAME", withObject: otherClassRef) { [weak self] otherClass in
            // Extract info 
            let data = otherClass.someData()
            self?.postingQueue.async { [weak self] in
                // Do something with Notification closure
                self?.processBus.sendEvent(data)
            }
        }
    }

}
```

## Combine

Listen Lifecycle event changes

```swift
import UIKit
import Combine

class MyFunkyViewController: UIViewController {

    /// The cancel bag containing all the subscriptions.
    private var cancelBag: Set<AnyCancellable> = []

    override func viewDidLoad() {
        super.viewDidLoad()
        addSubscribers()
    }

    /// Adds all the subscribers.
    private func addSubscribers() {
        NotificationCenter
            .Publisher(center: .default,
                       name: UIApplication.willEnterForegroundNotification)
            .sink { [weak self] _ in
                self?.doSomething()
            }
            .store(in: &cancelBag)
    }

    /// Called when entering foreground.
    private func doSomething() {
        print("Hello foreground!")
    }
}
```

https://stackoverflow.com/questions/25716012/triggering-a-specific-action-when-the-app-enters-foreground-from-a-local-notific

## Resources

https://dmytro-anokhin.medium.com/notification-in-swift-d47f641282fa

XPC Inter-process communication
https://developer.apple.com/documentation/xpc