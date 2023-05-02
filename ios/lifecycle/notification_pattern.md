# Notification  Pattern


## Default


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