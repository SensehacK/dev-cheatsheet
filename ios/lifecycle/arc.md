# ARC

Automatic Reference Counting

## Intro

Value and Reference type comes into picture as always. Number one culprit is the closures  which are reference type by nature will retain the strong reference (which is default) and thus when you're referencing self or inherently something is referencing self then you create a Retain Cycle.



## Retain Cycle

You can read up more on this [retain_cycle post.](retain_cycle.md)

When to use weak capture list to break the retain cycle.[unowned_vs_weak](unowned_vs_weak.md)


## Advance

Optimization on Swift

[Github markdown](https://github.com/apple/swift/blob/main/docs/ARCOptimization.md)

## Memory Graph

It is a great tool to quickly identify things across the application lifecycle. It create a graph like structure which shows strong or weak references of the objects currently in flight. You can also check if there are more objects being still in the memory after they have been dismissed or replaced by the navigation View controller by replacing or pushing one more view.

If the navigation uiview / uiviewcontroller stack is empty then by default swift / uikit / appkit or objective c runtime should automatically check the references and if the references are 0 zero then ARC (automatic reference counting) should do its job to deallocate those objects. 

I still remember the C / C++ days of unsafe pointers, `malloc` to allocate some memory and in order to save a string we needed to allocate each character byte to store a string. How far we have come in programming that an Open AI - Chat GPT 3 / 4 tool can easily generate code for us. Boilerplate code or just getting more information from the search engine but still cool nonetheless.
Objective C internally still has ways of Manual Memory management I believe. More control.

Memory Graph Debugger
[memory-graph-debugging-in-xcode](https://agostini.tech/2018/12/09/memory-graph-debugging-in-xcode/)

## Memory Management

How Heap and Stack memory work in Swift. 
[Article](https://heartbeat.fritz.ai/memory-management-in-swift-heaps-stacks-baa755abe16a)

### Memory Leaks Instrument

[raywenderlich | ARC in Swift](https://www.raywenderlich.com/966538-arc-and-memory-management-in-swift)


[medium | memory-management-in-swift-debugging-issues](https://medium.com/fueled-engineering/memory-management-in-swift-debugging-issues-53696fa7d8ae)


### Advance memory management

[apple dev | Cocoa memory management](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html#//apple_ref/doc/uid/10000011i)


Transition from Obj - C to ARC

[apple dev | Manual alloc - dealloc for references](https://developer.apple.com/library/archive/releasenotes/ObjectiveC/RN-TransitioningToARC/Introduction/Introduction.html)


[apple dev | Managing lifetime of Objects from Nib Files](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/LoadingResources/CocoaNibs/CocoaNibs.html#//apple_ref/doc/uid/10000051i-CH4-SW6)


## Storyboard

IBOutlets being referenced as weak references since the main parent object would be strong reference and it would deallocated all of its child IBOutlets when it goes off its screen.

iOS 6 also deprecated `-viewDidUnload` which was used before in Obj - C to set the UIViews to nil


```objc
self.aSubView = nil;
```

[SO | xcode-create-a-weak-reference-for-an-iboutlet](https://stackoverflow.com/questions/21654113/why-does-xcode-create-a-weak-reference-for-an-iboutlet)




## Closures

### Inner Outer Closures

```swift
// Memory leak
.sink { [localDatabase] value in
 

private func observeOutput() {  
    remoteDataSource.sampleData  
        .sink { [unowned self] value in // now there's no retain cycle  
            self.localDatabase.save(result: value) { [weak self] in  
                self?.activityIndicator.stopAnimating()  
                self?.showAlert()  
            }  
        }  
    .store(in: &subscriptions)  
}
```
It turns out that when we add `[weak self]` in the inner closure, we need to provide a `weak reference` to `self` for the outer closure as well. If we don’t provide any, `strong reference` will be used implicitly and we’ll **get a retain cycle**.

[fix retain cycle in nested closures swift](https://medium.com/@alexander100s124/fix-retain-cycle-in-nested-closures-in-swift-5e8152ea1690)

## Tasks

Swift Tasks implicitly capture strong self 

```swift
class MyClass {
    var myClosure: (() -> Void)?
    deinit { print("deinit MyClass") }
}

class MyViewController: UIViewController {
    var mc: MyClass!
    override func viewDidLoad() {
        super.viewDidLoad()
        mc = MyClass()
        mc.myClosure = {
            Task { [weak self] in
                // Do something with weak self
            }
        }
    }
    deinit { print("deinit MyViewController") }
}
```


adding `[weak self]` to the inner closure causes the outer closure to capture `self` strongly, which doesn't happen otherwise.
So the fix should be 
- Either don't capture weak self in inner `Task` closure
- Or capture weak self in outer closure. 

```swift
mc.myClosure = { [weak self] in 
	// do something
}
// OR
mc.myClosure = { 
	Task { 
	// do something
	}
}
```

Code snippet from [swift forums](https://forums.swift.org/t/unexpected-memory-leak-when-using-task-in-a-closure-causes/66272)

[iOS 17 memory leaks with SwiftUI](https://stackoverflow.com/a/77383133/5177704)
This gets fixed if we not use `fullscreenCover` and opt in for `push` view controller instead.

## References

[swift docs | ARC](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/automaticreferencecounting/)

[swift by sundell | swifts-closure-capturing-mechanics](https://www.swiftbysundell.com/articles/swifts-closure-capturing-mechanics/)

[Weak Self in Swift Made Easy: What it is and why it’s needed](https://matteomanferdini.com/swift-weak-self/)

[Two ways of capturing self strongly within a closure](https://www.swiftbysundell.com/articles/two-ways-of-capturing-self-strongly/)


