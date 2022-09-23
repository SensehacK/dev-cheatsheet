# Merge

Merging Observables


## Merge to one type

When we want different listeners from different types to be converted into a same type moving forward we can append `.withLatestFrom(Type_we_want_to_return)` 

```swift
let loadingDashboard = Observable
    .merge(
        loadDashboardSubject.distinctUntilChanged(), //1
        refreshDashboardElementsActionSubject.withLatestFrom(loadDashboardSubject), //2
        expandedDashboardDeveloperSetting.distinctUntilChanged().withLatestFrom(loadDashboardSubject) //3
    )
    .share()
```

The first `//1` is of type `DashboardContext` and it gets appropriately merged to return the specific type
The second `//2` is of type `BehaviorSubject<Void>` but when we tact it with `withLatestFrom` I'm assuming it returns `DashboardContext` since we add `dashboardSubject` 
The third `//3` is also the same when the actual type is `enum DeveloperSettings.ExpandedDashboard: Int` still we can do the same thing done in second statement.

So we can trigger from different types in order to run specific rx chain by soft mapping (maybe) or typecasting it using certain operator in order to keep the Observable<Type> of one type to use it forward.

## Discussion on Slack

Around roping in other observables into current stream to have 2 inputs rather than just one.

```text
.withUnretained() is used to capture a weak reference to an object that would otherwise be strongly captured and would require a [weak objectToCapture] explicit capture

JERSH 
.withLatestFrom() let’s you integrate the latest element from another observable into the source observable

kautilya 
Yep I knew the difference but I was having trouble roping in both Observables to map them appropriately.
postLoginSuccess.withLatestFrom(asrt)
            .map { accountContext in
I wanted to have two variables in map { type1LatestFrom, type2LoginSuccess in } (edited) 

JERSH  9 minutes ago
use .combiningLatestFrom() (might still be called .withLatestCombined() in your branch) (edited) 

JERSH  6 minutes ago
most of the combinational operators take an optional transform closure that lets you essentially perform a map, and .combiningLatestFrom() is just a convenience wrapper we wrote to make returning a tuple containing the latest elements from each observable a bit cleaner

JERSH  6 minutes ago
func combiningLatestFrom<T>(_ observable: Observable<T>) -> Observable<(Element, T)> {
    return withLatestFrom(observable) { ($0, $1) }
}

JERSH  6 minutes ago
the default implementation of .withLatestFrom() only returns the element from the observable sequence you pass into that operator

JERSH  5 minutes ago
which is equivalent to passing this to it’s optional transform closure
New

JERSH  4 minutes ago
Observable
    .of(37)   // Observable<Int>
    .withLatestFrom(.of("thirty seven")) { $1 } // Observable<String>
    
```