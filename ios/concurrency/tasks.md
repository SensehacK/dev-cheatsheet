# Tasks

## Intro

Could be described as a single unit of work needed to be completed could be described as a task.
Don't confuse this with process, threads, CPU Core.

Those are more of combination of multiple tasks -> Thread

Multiple threads + resources -> Process

Multiple threads could run on single core.

Multiple processes could run on single core.

## Code 

Swift Concurrency Task example
Task allows us to create concurrent tasks and call that from a non concurrent method using `async/await`.

```swift
let basicTask = Task {
    return "This is the result of the task"
}
print(await basicTask.value)
```

Lots of more examples of Task part of concurrency framework. WWDC 2021.  
[avanderlee | concurrency Tasks](https://www.avanderlee.com/concurrency/tasks/)

## Context Switching

CPU context switching happens using different time sharing / slicing algorithms and OS handles the priority of things to queue up to make sure efficient usage of limited resources at its disposal.

Now the strategy for handling resources would differ by lot of factors. 
Architecture CPU - arm, arm64, intelx86, amd64, RISC-V.
I/O - DDR2, 3, 4, LPDDR, SSD, Nand, eMMC, UFS, M.2 NVME, Hard Drives SATA 2, 3.
CPU Cache - L1, L2, L3
ECC Memory
Hardware accelerators
Security Modules - TPM, Apple T1, T2 chips, Enterprise Encryption
OS security - Encryption, Hardware encryption.

My point is Architecture isn't easy and there are lots of trade offs for every decision we make.

One could prefer Windows, macOS (unix subsystem), Debian flavored Linux, LinuxSE, Ubuntu.
UI - KDE plasma, Gnome, Windows Start, MacOS Springboard / launchpad / dock.

Btw I use `Arch` Linux.  **r/linuxMasterRace** meme

## Delay in Task

Adding a [timer](../ios/lifecycle/timer.md) in Swift language doc

### Async context

```swift
func foo() async {
    try await Task.sleep(nanoseconds: UInt64(seconds * Double(NSEC_PER_SEC)))
    // Put your code which should be executed with a delay here
}
```

[how to create a delay in swift SO](https://stackoverflow.com/questions/27517632/how-to-create-a-delay-in-swift)


```swift

let loadingSpinnerTask = Task {
	try await Task.sleep(nanoseconds: 150_000_000)
	showLoadingSpinner()
}

Task {
	await prepareVideo()
	loadingSpinnerTask.cancel()
	hideLoadingSpinner()
}

```



[delaying-an-async-swift-task | swift by sundell](https://www.swiftbysundell.com/articles/delaying-an-async-swift-task/)

### GCD

```swift
DispatchQueue.main.asyncAfter(deadline: .now() + seconds) {
    // Put your code which should be executed with a delay here
}
```

[Delay A Function Call and Sleep A Thread in Swift](https://www.advancedswift.com/delay-function-sleep-thread-swift/)

## Articles 

[SwiftUI Tasks vs OnAppear](https://byby.dev/swiftui-task-vs-onappear) 


## Reference

It would be good to maintain a reference to the task so it could be cancelled at any time.

1. Ensures there aren't multiple tasks happening at the same time
2. gives you something to kill on dealloc



## Result Type

Code snippet from [HWS](https://www.hackingwithswift.com/quick-start/concurrency/how-to-get-a-result-from-a-task)

```swift
enum LoadError: Error {
    case fetchFailed, decodeFailed
}

func fetchQuotes() async {
    let downloadTask = Task { () -> String in
        let url = URL(string: "https://hws.dev/quotes.txt")!
        let data: Data

        do {
            (data, _) = try await URLSession.shared.data(from: url)
        } catch {
            throw LoadError.fetchFailed
        }

        if let string = String(data: data, encoding: .utf8) {
            return string
        } else {
            throw LoadError.decodeFailed
        }
    }

    let result = await downloadTask.result

    do {
        let string = try result.get()
        print(string)
    } catch LoadError.fetchFailed {
        print("Unable to fetch the quotes.")
    } catch LoadError.decodeFailed {
        print("Unable to convert quotes to text.")
    } catch {
        print("Unknown error.")
    }
}

await fetchQuotes()
```


## Do try catch Errors 

```swift
func fetchUpdates() async {
    let newsTask = Task { () -> Data in
        let url = URL(string: "https://hws.dev/headlines.json")!
        let (data, _) = try await URLSession.shared.data(from: url)
        return data
    }

    let highScoreTask = Task { () -> Data in
        let url = URL(string: "https://hws.dev/scores.json")!
        let (data, _) = try await URLSession.shared.data(from: url)
        return data
    }

    do {
        let news = try await newsTask.value
        let highScores = try await highScoreTask.value
    } catch {
        print("There was an error loading user data.")
    }
}

await fetchUpdates()
```

[Hacking with Swift | Create a task](https://www.hackingwithswift.com/quick-start/concurrency/how-to-create-and-run-a-task)

[SO | throwing errors in tasks](https://stackoverflow.com/questions/70314263/throwing-errors-inside-a-root-task)


## Yield | Suspend


```swift
await Task.yield()
```

[HWS | voluntarily suspend a task](https://www.hackingwithswift.com/quick-start/concurrency/how-to-voluntarily-suspend-a-task)




## Mind Map

[ARC in Tasks | Reference Counting](arc.md#Tasks)

## Swift UI Tasks

> SwiftUI provides a `task()` modifier that starts a new task as soon as a view appears, and automatically cancels the task when the view disappears. This is sort of the equivalent of starting a task in `onAppear()` then cancelling it `onDisappear()`, although `task()` has an extra ability to track an identifier and restart its task when the identifier changes.

[HWS | runs tasks with SwiftUI lifecycle](https://www.hackingwithswift.com/quick-start/concurrency/how-to-run-tasks-using-swiftuis-task-modifier)

```swift
// Equatable 
struct Message: Decodable, Identifiable {
    let id: Int
    let user: String 
}
@State private var messages = [Message]()

NavigationStack {
	// DO UI Stuff
}
.task {
	await fetchData()
}


 func fetchData() async {
	do {
		let url = URL(string: "https://hws.dev/inbox.json")!
		let (data, _) = try await URLSession.shared.data(from: url)
		messages = try JSONDecoder().decode([Message].self, from: data)
	} catch { }
	

// Async Tasks
struct NumberGenerator: AsyncSequence, AsyncIteratorProtocol {

mutating func next() async -> Int? { 
	while Task.isCancelled == false {
		return Int.random(in: 1...500)
	}
	return nil
}

func makeAsyncIterator() -> NumberGenerator { self }

}

@State private var numbers = [String]()
let generator = NumberGenerator()

NavigationStack { }
.task {
	await generateNumbers()
}

func generateNumbers() async {
	for await number in generator {
		numbers.insert("\(numbers.count + 1). \(number)", at: 0)
	}
}
```




## Task as property

Various ways to get the task or subscript task or await async state in a function with retrieve reusability in mind.

```swift
final class AdBeaconWrapper {
    private(set) var adBreakContainer: Set<AdBreakContainer> = []
    fileprivate var adMapProvider: AdMapProvider
   
    func retrieveCurrentAdBreak(_ timelineSegment: TimelineSegment) -> EntosAd.AdBreak? {
        guard let currentAdContainer = retrieveCurrentAdContainer(timelineSegment) else {
            log("Cant find Ad container for associated unique ID", level: .warning)
            return nil
        }

        return currentAdContainer.entOsAdBreak
    }
}

```

```swift
final class AdBeaconWrapper {
    subscript(adBreak segment: TimelineSegment) -> EntosAd.AdBreak {
        get async throws {
            let retrieveAdBreak: Task<EntosAd.AdBreak, Swift.Error> = Task {
                guard let adBreak = retrieveCurrentAdBreak(segment) else {
                    throw AdBeaconError.couldntEmitAdBreak
                }
                return adBreak
            }

            return try await retrieveAdBreak.value
        }
    }


    func prepare(segment: TimelineSegment) {
    	Task {
            let adBreak = try await self[adBreak: segment]
        }
    }
}


```swift
final class AdBeaconWrapper {
    func prepare(segment: TimelineSegment) {
    	let retrieveAdBreak: Task<EntosAd.AdBreak, Swift.Error> = Task {
            guard let adBreak = retrieveCurrentAdBreak(segment) else {
                throw AdBeaconError.couldntEmitAdBreak
            }
            return adBreak
        }

    	Task {
            let adBreak = try? await retrieveAdBreak.value
        }
    }
}
```


```swift
final class AdBeaconWrapper {
	lazy var retrieveSetOut: Task<Set<AdBreakContainer>, Never> = Task {
        adBreakContainer = await adMapProvider.getAdBreakContainer()
        return adBreakContainer
    }

    func prepare(segment: TimelineSegment) {
    	let retrieveSet: Task<Set<AdBreakContainer>, Never> = Task {
            adBreakContainer = await adMapProvider.getAdBreakContainer()
            return adBreakContainer
        }

    	Task {
            let adBreak = try? await retrieveSet.value

            let adbreakContainer = await retrieveSetOut.value
        }
    }
}
```swift

