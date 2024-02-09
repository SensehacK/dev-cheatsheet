

###  class instance vs value reference

cast it from kindofclass HelioPlayer PlayerEngine

objectiveC


check

```objc
class CDelegate { }

class anotherClass {
	let cDelegate = CDelegate()
	
	_cDelegate
	// vs 
	self.cDelegate
}
```


## Errors

Code snippet where this error appears

```objc
@protocol CDelegate <NSObject>
@required
- (void)handleChange:(NSString *)result;
@end
```
```swift
final class MockDelegate: CDelegate {
}
```

```sh
Cannot declare conformance to 'NSObjectProtocol' in Swift; 'MockDelegate' should inherit 'NSObject' instead
```

Explicitly conforming to `NSObject` will fix this issue.

```swift
final class MockDelegate: NSObject, CDelegate {
}
```

This happens because  `CDelegate` itself inherits from `NSObjectProtocol` therefore you need to implement methods in that protocol, too. The easiest way to implement those methods is to subclass `NSObject`:
[SO | Post](https://stackoverflow.com/questions/40705591/class-does-not-conform-nsobjectprotocol)


## Forward class declaration

```swift
@class CDelegate2;
@protocol CDelegate;


@objc
public protocol CDelegate: AnyObject {
    func handleChange(result: String)
}
@objc class CDelegate2 { }
```

Current Teammate explaining it - [Ray](misc/resources#Offline)
A forward class declaration is simply an instruction to the compiler that “this thing exists, I’m going to annotate some functions and instance vars with it, but you don’t need to know anything else at this time”When it comes to an implementation and you start needing methods and properties of that class, you must import the header containing those details 

[Article](https://railsware.com/blog/using-forward-declaration-in-your-objective-c-projects/) 

[SO | explaining it](https://stackoverflow.com/questions/5191487/objective-c-forward-class-declaration)

[Apple dev | importing swift in ObjC](https://developer.apple.com/documentation/swift/importing-swift-into-objective-c)