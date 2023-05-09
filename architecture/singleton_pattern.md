# Singleton

## Pros

- Easy understanding
- One source of truth
- Object remains in the memory throughtout the app lifecycle.
- Supports lazy initialization. 
- Used by lot of analytics SDKs
- iOS UIKit, CocoaTouch relies a lot on Singleton and MVC pattern.
- App Delegate is important singleton instance.

## Cons 

- Data inconsistency - Not multi thread safe. (Not good for CRUD operations)
- More dependencies - Highly coupled
- Less testable
- Breaks SOLID - Single responsibility (Does too many things, Concrete implementation)
- Gets overuse quickly.
- If you have lots of singletons for App Delegate or Scene Delegate.
- Could be time dependent with some callback.


## Code

Important to privatize the initi() in order to not let invocation rights to anyone else.

```swift
class SingletonClass { 
	static let shared: SingletonClass = SingletonClass()

	private init() { }

	func foo() { }	 
}
```

Also defining the class `final` and having just `Singleton` pattern for invocation only once is kind of similar but there is definitely need for each in their own right.


## References

I know Java has few differences & I haven't taken my time to research these things in iOS Swift world.

https://stackoverflow.com/questions/519520/difference-between-static-class-and-singleton-pattern?rq=1

https://stackoverflow.com/questions/51508613/is-final-necessary-for-a-singleton-class-in-swift


https://javarevisited.blogspot.com/2013/03/difference-between-singleton-pattern-vs-static-class-java.html

https://medium.com/@nimjea/singleton-class-in-swift-17eef2d01d88

https://www.swiftbysundell.com/tips/quickly-replacing-singletons-with-functions/