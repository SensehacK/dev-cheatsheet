Unowned vs Weak Reference




Good Stack overflow explanation

[SO](https://stackoverflow.com/questions/25377674/unowned-vs-weak-why-we-should-prefer-unowned)
unowned vs. weak. Why we should prefer unowned?


Weak references are automatically set to nil once the object they point to gets deallocated. For this to be possible in Swift, those must be declared as var and optional:
```swift
class SomeOtherClass {
    weak var weakProperty: SomeClass?
}
```

This is fine if the weakProperty can become nil while the instance of SomeOtherClass is still alive and we want to check for that before using it (delegates are one such example). But what if some reference should never logically be nil and we still want to prevent a retain cycle? In Objective-C any object reference can be nil (and messaging nil always fails silently) so there is no dilemma, we always use weak. But Swift doesn't have nilable references at all. We use optionals for something that can semantically lack value. But we shouldn't be forced to use optionals for something that must always have value, just to be able to break a retain cycle. Such practice would go against the intended semantics of optionals.

That's where unowned comes in. It comes in two flavours - unowned(safe) and unowned(unsafe). The latter is dangerous and it's equivalent to assign and unsafe_unretained from Objective-C. But the former, which is the default one (at least while debugging; not sure if they optimise it to unowned(unsafe) in release builds), will reliably crash your app if the referenced object gets prematurely deallocated. Sure, your app will crash if something goes wrong, but that's much easier to debug than failing silently. It should only fail silently when you actually want that (in which case you would use weak)

## Self 

https://stackoverflow.com/questions/39433221/why-do-closures-require-an-explicit-self-when-theyre-all-non-escaping-by-defa


## Weak

When you're not sure whether certain instance would be present at that time in a closure which could outlive its parent invocation. Then you should use `[weak self]` capture list in closures in order to not create [retain_cycle](retain_cycle.md) as well as not crashing the app if the instance you're trying to access isn't present.


Pros:
- Safe
- Easy understanding
- Preferred way

Cons:
- Performance cost
- Always `Optional` self so the code looks ugly `self?.doSomething()`
- Easily ^ avoidable using `guard let self = self else { return }`


## Unowned

Pros:
- Performance faster as no overhead of checking reference valid
- Doesn't look ugly with code `self?.` vs `self` 

Cons:
- Not Safe
- Harder understanding
- Always `Optional` self so the code looks ugly `self?.doSomething()`




## References

https://www.swiftbysundell.com/articles/swifts-closure-capturing-mechanics/

https://medium.com/@almalehdev/you-dont-always-need-weak-self-a778bec505ef
