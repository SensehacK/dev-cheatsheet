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

It is a great tool to quickly identify things across the application lifecycle. It creats a graph like structure which shows strong or weak references of the objects currently in flight. You can also check if there are more objects being still in the memory after they have been dismissed or replaced by the navigation View controller by replacing or pushing one more view.

If the navigation uiview / uiviewcontroller stack is empty then by default swift / uikit / appkit or objective c runtime should automatically check the references and if the references are 0 zero then ARC (automatic reference counting) should do its job to deallocate those objects. 

I still remember the C / C++ days of unsafe pointers, `malloc` to allocate some memory and in order to save a string we needed to allocate each character byte to store a string. How far we have come in programming that an Open AI - Chat GPT 3 / 4 tool can easily generate code for us. Boilerplate code or just getting more information from the search engine but still cool nonetheless.
Objective C internally still has ways of Manual Memory management I believe. More control.

Memory Graph Debugger

https://agostini.tech/2018/12/09/memory-graph-debugging-in-xcode/



## Memory Management

How Heap and Stack memory work in Swift. 
[Article](https://heartbeat.fritz.ai/memory-management-in-swift-heaps-stacks-baa755abe16a)

### Memory Leaks Instrument

https://www.raywenderlich.com/966538-arc-and-memory-management-in-swift

https://medium.com/fueled-engineering/memory-management-in-swift-debugging-issues-53696fa7d8ae

### Advance memory management
https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html#//apple_ref/doc/uid/10000011i

Transition from Obj - C to ARC

Manual alloc - dealloc for references
https://developer.apple.com/library/archive/releasenotes/ObjectiveC/RN-TransitioningToARC/Introduction/Introduction.html

Managing lifetime of Objects from Nib Files
https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/LoadingResources/CocoaNibs/CocoaNibs.html#//apple_ref/doc/uid/10000051i-CH4-SW6

## Storyboard

IBOutlets being referenced as weak references since the main parent object would be strong reference and it would deallocated all of its child IBOutlets when it goes off its screen.

iOS 6 also deprecated `-viewDidUnload` which was used before in Obj - C to set the UIViews to nil

```objectivec
self.aSubView = nil;
```
 
https://stackoverflow.com/questions/21654113/why-does-xcode-create-a-weak-reference-for-an-iboutlet


## References

https://docs.swift.org/swift-book/documentation/the-swift-programming-language/automaticreferencecounting/
