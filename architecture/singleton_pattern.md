## Singleton

Pros:
- Easy understanding
- One source of truth
- Object remains in the memory throughtout the app lifecycle.
- Supports lazy initialization. 
- Used by lot of analytics SDKs
- iOS UIKit, CocoaTouch relies a lot on Singleton and MVC pattern.
- App Delegate is important singleton instance.

Cons:
- Data inconsistency - Not multi thread safe. (Not good for CRUD operations)
- More dependencies - Highly coupled
- Less testable
- Breaks SOLID - Single responsibility (Does too many things, Concrete implementation)
- Gets overuse quickly.
- If you have lots of singletons for App Delegate or Scene Delegate.
- Could be time dependent with some callback.


```swift

class SingletonClass { 
	static let shared: SingletonClass = SingletonClass()

	private init() { }

	func foo() { }	 
}

