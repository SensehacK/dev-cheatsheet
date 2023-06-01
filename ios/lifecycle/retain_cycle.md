# Retain Cycle


## Intro

When object A -> holds a strong reference to Object B. 
And Object B -> holds a strong reference to Object A.
Multiple objects can be present but the important concept is it is cyclic dependency graph or a retain cycle since Apple - Swift runtime execution always defaults to strong reference object types.



## Identify

Only classes and closures are reference types in Swift.
Everything else is mostly value type.
Now `actors` are the exeption which was recently introduced.

As long as you reference a reference object in a closure body by default it captures strong so to avoid that you can capture them in the closure block syntax

## Mitigate

Avoiding retain cycle by capturing self if being referenced in the closure. By making it weak object reference using `weak` or `unowned` is the way to break the cyclic dependency graph or retain cycle

Possible Retain Cycle
```swift
class ParentClass {
	anotherFunction() { print("Callback!")}
	
	SomeClass()
	.functionCompletioner { 
		self.anotherFunction
	}
}
```

Breaking Retain Cycle
```swift
class ParentClass {
	anotherFunction() { print("Callback!")}
	
	SomeClass()
	.functionCompletioner { [weak self] in
		self?.anotherFunction
	}
}
```


You can read up on when to use weak or unowned in this [unowned_vs_weak post.](unowned_vs_weak.md)


## Basic errors

Protocol with weak references
[SO](https://stackoverflow.com/questions/33471858/swift-protocol-error-weak-cannot-be-applied-to-non-class-type)





## Retain cycle

https://stackoverflow.com/questions/19892245/understanding-retain-cycle-in-depth

## Sources


[avoiding retain cycle](https://medium.com/mackmobile/avoiding-retain-cycles-in-swift-7b08d50fe3ef)

https://medium.com/wolox/how-to-automatically-detect-a-memory-leak-in-ios-769b7bb1ec7c

[Memory graph](https://doordash.engineering/2019/05/22/ios-memory-leaks-and-retain-cycle-detection-using-xcodes-memory-graph-debugger/)
https://medium.com/swift2go/how-i-stopped-that-memory-leak-and-reclaimed-150mb-of-memory-swift-3631f522d249
