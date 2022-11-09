


## NSObject
Inheritance towards Class and not extension of that class.
Inherit to NSObject in the base class implementation.

When you have conform to a specific protocol for its delegate callbacks and the protocol internally also needs to be conformed with `NSObject`  where `AnyClass: NSObject` maybe. 

Then you would have to inherit to your class `YourClassNameHere: NSObject` and not on `extension YourClassNameHere: NSObject` 
Also you would need to call in `super.init()` in its initializer.


Example of WKWebview Delegate

```swift
import WebKit
final class YourClassNameHere: NSObject {
	
	init() {
	super.init()
	// reference self afterwards
	}

}

extension YourClassNameHere: WKScriptMessageHandler {
	
	func userContentController(_ userContentController: WKUserContentController, didReceive message: WKScriptMessage) { 
		print("Delegate method called")
	} 
	
}
```

`Inheritance from non-protocol type 'NSObject'`  - Don't inherit to a protocol.

If you have lot of protocol conformance autocomplete stubs in class declaration then don't try to subclass `NSObject` in that class' extension. `extension YourClassNameHere: NSObject`


## Reference


https://stackoverflow.com/questions/24650325/why-in-swift-we-cannot-adopt-a-protocol-without-inheritance-a-class-from-nsobjec

https://stackoverflow.com/questions/40705591/class-does-not-conform-nsobjectprotocol?noredirect=1&lq=1

https://www.hackingwithswift.com/read/10/5/custom-subclasses-of-nsobject