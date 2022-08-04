# Concurrency

Basic concepts from my understanding.


## Multi Threading | Multi Processing

I know they defer a lot when we really want to go into the weeds of Operating Systems, Kernel implementation or resource allocation with respect to hardware I/O. But for the sake of argument just coupling them together for normal conversations. Don't want to open a pandora's box to further complicate this. 

Side note: You can do multi threading on a single processor or do multi tasking (smart context switching) on a single thread or processor - windows 95 or 98 introduced it long time ago I believe.


## Async vs Sync

When a piece of work, process, thread, code, executable (machine code) is meant to execute in a blocking or non blocking way. 

### Async: 

For example your heart beats in an async fashion it isn't dependent retrospectively for someone's input in order to make the next heart beat to pump blood in your veins  of the human body.

### Sync: 

On the other hand eyes, brain coordinate with each other to send a neuron signal via synapses in order for the human motor functions to operate. So that is in a way synchronous activity. Hands or other body functions are dependent on some other functions when they give signals to do certain task synchronously and when they are doing certain task they do it in somewhat blocking way. Of course human brain is somewhat more capable of scheduling multiple instances of parallel activities such as your mental intuition is still in the works, your five sensory inputs are still working in the background and more.

I should have went with a better example since human body mostly works asynchronously for most tasks and does it in a multi processing state. Well I wanted to try explaining it from a human mind's perspective.


## Thread 

A unit of work to be executed by a processor.
Multiple threads can exist on a single process.

## Process

A collection of threads or units of work to be executed by the OS scheduler is called a process. It may also include shared resources in order to better communicate with other processes or access low level apis with kernel or I/O devices.

## Scheduler

It is a special set of computer program or logic which handles how certain processes or computer instructions gets executed in a way while considering various thresholds, priorities, resources available, I/O considerations, interrupts etc. Scheduler's job in the end is to be as efficient as possible in order to fulfilled maximizing the resources at a given time so it can complete the task as quick as possible.
