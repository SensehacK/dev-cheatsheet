# Notification  Pattern

## Add Observer

Adding the notification observer is easy and we use singleton pattern to get `default` context from Notification Center. We can specify the `name` or `class object` 
You can specify the closure to expand right away or pass 
in another [closure](../../ios/swift/closure.md)

```swift
func listenObserver() {
    NotificationCenter
    .default
    .addObserver(
	    forName: Notification.Name(rawValue: notificationName),
	    object: object, 
	    queue: nil, 
	    using: closure
	)
}
```

Selector option with `addObserver`
```swift
NotificationCenter
    .default
    .addObserver(
	    self,
	    selector: #selector(post), 
	    name: Notification.Name(rawValue: notificationName),
	    object: nil
	)

@objc 
func post() { }
```

## Remove Observer

Normal removal of observer
```swift
NotificationCenter.default.removeObserver(self)
```

```swift
NotificationCenter.default.removeObserver(Notification.Name)
```
When removing an observer, remove it with the most specific detail possible. For example, if you used a name and object to register the observer, use [`removeObserver(_:name:object:)`](https://developer.apple.com/documentation/foundation/notificationcenter/1407263-removeobserver) with the name and object.

[apple doc](https://developer.apple.com/documentation/foundation/notificationcenter/1413994-removeobserver#discussion)



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

	func deinit() {
		cancelBag.removeAll()
	}
}
```

[SO | triggering  action app-enters-foreground-from-a-local-notific](https://stackoverflow.com/questions/25716012/triggering-a-specific-action-when-the-app-enters-foreground-from-a-local-notific)


## Behavior

### Twice notifications firing

> I don't know wether the solution is correct or not but if 'obj' is a @State variable and there is a value change for @State variable it may execute the same line again i.e., NotificationCenter.default.post(name: .helloStack, object: obj)

For me it was having two emits `.sink` block when I was updating the AVPlayer.currentItem twice

```swift
let lplayerItem = MockAVPlayerItem(url: testUrl)
let lplayer = MockAVPlayer()

// This statement was making my sink block fire twice
lplayer.replaceCurrentItem(with: lplayerItem)

lbus.events
	.print("Hello playerITEM ####")
	.filter { $0.type == .playerItemTimeJumped }
	.sink { event in
		print("$$$")
		XCTAssertEqual(event.description, "AVPlayer Item Time Jumped")
		expectation.fulfill()
	}

NotificationCenter.default
	.post(name: AVPlayerItem.timeJumpedNotification, 
	object: lplayer.currentItem)
```

[SO | Notification subscribe combine](https://stackoverflow.com/questions/69400510/swift-notificationcenter-publisher-subscriber-called-more-than-once)

## Resources

[Medium | Notifications in swift](https://dmytro-anokhin.medium.com/notification-in-swift-d47f641282fa)


[Apple Docs | XPC Inter-process communication](https://developer.apple.com/documentation/xpc)


