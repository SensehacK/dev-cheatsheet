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
