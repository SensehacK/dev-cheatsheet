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
