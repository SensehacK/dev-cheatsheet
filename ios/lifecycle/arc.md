# ARC


Automatic Reference Counting






## Advance

Optimization on Swift

[Github markdown](https://github.com/apple/swift/blob/main/docs/ARCOptimization.md)


## Memory graph 

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

