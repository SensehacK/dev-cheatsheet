
# Key - Value Observing

## KVO Observing
https://www.hackingwithswift.com/example-code/language/what-is-key-value-observing

https://nalexn.github.io/kvo-guide-for-key-value-observing/


## KVO to Combine

Any object which is NSObject and is key value observable could be used with combine's publisher.  `NSObject.KeyValueObservingPublisher

Code Snippet from Apple docs

```swift
class UserInfo: NSObject {
    @objc dynamic var lastLogin: Date = Date(timeIntervalSince1970: 0)
}
@objc var userInfo = UserInfo()
// KVO
var observation: NSKeyValueObservation?
// Combine
var cancellable: Cancellable?


override func viewDidLoad() {
    super.viewDidLoad()
}


override func viewDidAppear(_ animated: Bool) {
    super.viewDidAppear(animated)
    userInfo.lastLogin = Date()
}

func observeKVOWay() {
	observation = observe(\.userInfo.lastLogin, options: [.new]) { object, change in
        print ("lastLogin now \(change.newValue!).")
    }			  
}

func combineKVOWay() {
	cancellable = userInfo.publisher(for: \.lastLogin)
        .sink() { date in print ("lastLogin now \(date).") }
	}			  
}
```


https://developer.apple.com/documentation/combine/performing-key-value-observing-with-combine






## UI KVO Combine Publisher

NotificationCenter.default.publisher can actually be utilized to make it more easier to listen to change events from UIKit. UI Kit doesn't provide KVO observing, it has the traditional `delegate` callback pattern, selector pattern or Notification Observer pattern

```swift
NotificationCenter
	.default
	.publisher(for: UISearchTextField.textDidChangeNotification,
				object: customSearchBar.searchTextField)
	.map { $0.object as? UISearchTextField)?.text }
	.debounce(for: .seconds(1), scheduler: DispatchQueue.main)
	.sink { [weak self] keywordStr in 
		print("Keyword: \(keywordStr)")
	}
	.store(in: &cancellable)

```
https://youtu.be/2ef3nlf13JU?si=BUmLEpnP_74WgYjV

https://stackoverflow.com/questions/58559908/combine-going-from-notification-center-addobserver-with-selector-to-notificatio




