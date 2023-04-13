Design Patterns


## MVC

Model View Controller

Pros:
- Apple's default implementation in Objective C and Swift UIKit.
- Easier for freshers.

Cons:
- Massive View controller
- Not unit testable to higher degree.
- ViewController does lot of things

## MVVM

[MVVM](MVVM.md)
Model View ViewModel

Doesn't define how VM communicates with VC and Model layer.
You can use Functional Reactive programming, KVO pattern, Closures, Delegate pattern

Swift UI embeds this thorougly.
Data Flow.
View controler  < - > View Model < - > Model

VM -> Speaks to View Controller.
VM -> Speaks to Model

Pros:
- VM - Business logic is seperate

- Easily testable
- Dependency Injection  | Seperation of Concerns
-  SOLID principles
- Promotes Reusuability accross diff platforms iOS, iPadOS, MacOS, WatchOS, Catalyst.
- Great with Reactive paradigm

Cons:
- View Controller still has bloated code.
- 





## Coordinator pattern

Navigation Coordinator pattern -> Passing around navigationContext to take care of presenting and dismissing logic from one point.


## MVVM - C

Pros: 
- Less presentation logic duplication
- Good global state management

Cons:
- Upfront cost
- Need to deal with multi level child VCs or View presenters
- Traverse [UIViews] or Views
- Singleton needed



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

```

## Facade pattern



## Delegate Pattern 


1 : 1 type


https://medium.com/@nimjea/delegation-pattern-in-swift-4-2-f6aca61f4bf5


Pros:
- No extra management of state. It is one to one.
- Less side effects.


Cons:
- Need to be one to one
- 


## Notification Pattern

1 - > N 

Pros:
- Broadcasting everything at once.
- Big state change and you need to reflect that everywhere.

Cons:
- Subscribing and disposing of subsribers
- Multiple firing of events.
- Hot / Cold observers