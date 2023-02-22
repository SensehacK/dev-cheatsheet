

## EXC_BAD_ACCESS

`Thread 1: EXC_BAD_ACCESS (code=1` in runtime - while using NavigationContext - Navigation Pattern passing around objects / context from one ViewController to another viewController. Like a dependency injection in the initializer.

I started noticing having this error popping up with different simulators.
Day 1 : 
My teammate suggested that he also used to have this error popup once in a while and suggested me to restart my Mac.
First time restart worked but the dreaded error appeared again & being a novice / intermediate in ReactiveIO RxSwift I thought I'm not intializing the properties or classes right way which leads to this error.
But even reverting my working changeset doesn't fix it and that led me to believe that this is not my code issue hopefully.

Day2:
When my teammate and I were pair programming, in that instance everything was working fine and the next commit or branch switching led to a dirty state and having commited few of changes to working branch. I was planning to revert them but my teammate checked out the branch and ran the same code which was commited by us and he wasn't able to get that error / runtime crash in his simulator.

Day 3: 
Again with this error. This time it popped up when I was passing around objects back and forth with MVVM pattern mixed with Navigation Coordinator pattern.
The error came back. Removed / Deleted the app from simulator & ran it again.
No avail.
Restarted my mac - didn't fix it.
Finally I thought maybe try `Clean Build Folder` and it worked fine after that.

The number of times an iOS Engineer has to go back to basics like 
- Manually clearing out Derived Data
- Clean Build Folder
- Deleting app on simulator
- Closing Xcode
- Force quitting Xcode
- Swift Package Manager - Reset package cache
- SPM - resolving packages
- Restarting Mac



## NSRangeException

Usually this is caused due to Array index out of bounds which means if the Array index is greater than the actual value
eg. 
```swift
var tempArray = [2,45,22,53,36]
// So if you want to access 2nd value of array
tempArray[1] // 45
// But if you access 6th value in the array when it doesn't exists
tempArray[5] // uncaught exception 'NSRangeException' | Out of bounds
```
This is the error message
```error
*** Terminating app due to uncaught exception 'NSRangeException', reason: 'NSMutableRLEArray replaceObjectsInRange:withObject:length:: Out of bounds'
terminating with uncaught exception of type NSException
CoreSimulator 857.14
```

But removing the app from the simulator and Xcode -> Clean Build also solved the problem if you're not able to determine why this is happening without any proper code change around indexes. Happened with me on Xcode 14.2 - iOS 16.2