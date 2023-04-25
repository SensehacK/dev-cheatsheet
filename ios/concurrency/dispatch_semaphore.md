
# Dispatch Semaphore

## Intro

Semaphores are a way to place safeguards and fine control to make sure certain part of a code is manually flagged for getting exclusive access at a given time. 
Dispatch_Barrier can achieve this but Semaphore gives you finer control on specifying where this conditions could be added and gives the OS or engineer more low level access for directing guard conditions at certain scenarios.

Need: Sometimes only few lines of code are needed to be guarded or have exclusive access so in those times `Dispatch_barrier` would be an overkill specifically when the function is smaller. These kind of shortcomings could be solved using `functional programming` and having every independent unit of task defined as a task / function.  And only limiting certain aspects for `semaphore.wait` and `sempahore.signal`.

## Code

### Initialization
```swift
// Init
let semaphore: DispatchSemaphore = DispatchSemaphore(value: 1)
```

## Toggle States

Engaging +1 and disengaging  -1 for the OS scheduler to take control of exclusion and make the right decision.
```swift
// Engage
semaphore.wait()

// DisEngage
semaphore.signal()
```

## Quirks

###  Priority Inversion

Where there are three tasks of different priorities `low, medium & high`. But when the execution happens the `high` priority is always waiting for the execution to happen for other 2 tasks. Thus the priority of a task not being honored.
