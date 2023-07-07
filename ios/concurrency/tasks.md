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
https://www.avanderlee.com/concurrency/tasks/



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
