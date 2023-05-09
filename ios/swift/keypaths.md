# KeyPaths


[Keypath Basics](https://sarunw.com/posts/what-is-keypath-in-swift/)

```swift
struct Feature { 
	let showView: Bool
	let showNotification: Bool
	let name: String			   
}
let features: [Feature] = [
	Feature(showView: true  , showNotification: false , name: "Kay"),
	Feature(showView: true  , showNotification: true , name: "Nay"),
	Feature(showView: true  , showNotification: false , name: "Say")
]

let showFeatureNotifications = features
	.map(\.showNotification)	

print(showFeatureNotifications) // [false, true, false]
```

Key - Value Coding

## Key - Value Observing

KVO Observing
https://www.hackingwithswift.com/example-code/language/what-is-key-value-observing

https://nalexn.github.io/kvo-guide-for-key-value-observing/

KVO to Combine

Any object which is NSObject and is key value observable could be used with combine's publisher.  `NSObject.KeyValueObservingPublisher

https://developer.apple.com/documentation/combine/performing-key-value-observing-with-combine