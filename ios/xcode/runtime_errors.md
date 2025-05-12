# Run time Errors


## EXC_BAD_ACCESS

`Thread 1: EXC_BAD_ACCESS (code=1` in runtime - while using NavigationContext - Navigation Pattern passing around objects / context from one ViewController to another viewController. Like a dependency injection in the initializer.

I started noticing having this error popping up with different simulators.
Day 1 : 
My teammate suggested that he also used to have this error popup once in a while and suggested me to restart my Mac.
First time restart worked but the dreaded error appeared again & being a novice / intermediate in ReactiveIO RxSwift I thought I'm not intializing the properties or classes right way which leads to this error.
But even reverting my working changeset doesn't fix it and that led me to believe that this is not my code issue hopefully.

Day2:
When my teammate and I were pair programming, in that instance everything was working fine and the next commit or branch switching led to a dirty state and having committed few of changes to working branch. I was planning to revert them but my teammate checked out the branch and ran the same code which was committed by us and he wasn't able to get that error / runtime crash in his simulator.

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


## EXC_BAD_ACCESS

```log
Crash: xctest (63466) withThrowingTaskGroup<A, B>(of:returning:isolation:body:)


Exception Type:  EXC_BAD_ACCESS (SIGSEGV)
Exception Subtype: KERN_INVALID_ADDRESS at 0x0000000000000004
Exception Codes: 0x0000000000000001, 0x0000000000000004
VM Region Info: 0x4 is not in any region.  Bytes before following region: 4366909436
      REGION TYPE                    START - END         [ VSIZE] PRT/MAX SHRMOD  REGION DETAIL
      UNUSED SPACE AT START
--->  
      __TEXT                      10449c000-1044a0000    [   16K] r-x/r-x SM=COW  /Applications/Xcode-16.2.0-Beta.2.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/Library/Xcode/Agents/xctest
Termination Reason: SIGNAL 11 Segmentation fault: 11
Terminating Process: exc handler [56073]

Triggered by Thread:  3

Thread 0::  Dispatch queue: com.apple.main-thread
```

Odd why this only happens on my Xcode 16.2 beta local build but this doesn't fail on CI build server which runs on Xcode 16 official release.


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
```sh
*** Terminating app due to uncaught exception 'NSRangeException', reason: 'NSMutableRLEArray replaceObjectsInRange:withObject:length:: Out of bounds'
terminating with uncaught exception of type NSException
CoreSimulator 857.14
```

But removing the app from the simulator and Xcode -> Clean Build also solved the problem if you're not able to determine why this is happening without any proper code change around indexes. Happened with me on Xcode 14.2 - iOS 16.2



