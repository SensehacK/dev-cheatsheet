## View State Bridger Protocol

```swift
protocol ViewStateBridger {
    associatedtype ViewStateType: ViewStateProtocol
    var viewState: Driver<ViewStateType> { get }
}

extension ViewStateBridger {
    var success: Observable<ViewStateType.SuccessType> { viewState.success.asObservable() }
    
    var error: Observable<ViewStateType.ErrorType> { viewState.error.asObservable() }
    
    var loading: Observable<ViewStateType.LoadingType> { viewState.loading.asObservable() }

    var empty: Observable<ViewStateType.EmptyType> { viewState.empty.asObservable() }
}
```


This ViewState Bridger protocol depends on `Driver` Extension you can find here.
[viewStateExtensions](viewStateExtensions.md) Where you need to navigate to `Driver` headline in order to properly compile.