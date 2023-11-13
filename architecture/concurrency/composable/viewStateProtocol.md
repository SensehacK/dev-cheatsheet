

## Protocol ViewState

```swift
protocol ViewSuccess { }
protocol ViewErrable { }
protocol ViewLoadable { }
protocol ViewEmptiable { }

extension Never: ViewSuccess, ViewErrable, ViewLoadable, ViewEmptiable { }

protocol ViewStateProtocol {
    associatedtype SuccessType: ViewSuccess
    associatedtype ErrorType: ViewErrable
    associatedtype LoadingType: ViewLoadable
    associatedtype EmptyType: ViewEmptiable
    
    var success: SuccessType? { get }
    var error: ErrorType? { get }
	var loading: LoadingType? { get }
    var empty: EmptyType? { get }
}
```


## Empty States
When you need to have empty initializer just to conform to the type of ViewState Protocols. You can utilize these memberless structs in your Generic initializer.

```swift
public struct SuccessState: ViewSuccess { init() { } }

public struct ErrorState: ViewErrable { init() { } }

public struct LoadingState: ViewLoadable { init() { } }

public struct EmptyState: ViewEmptiable { init() { } }
```

So if you want default init() without any states you can invoke these by using. Since any ViewController and ViewModel conforming to `ViewStateBridger` would need this type defined from `ViewModel` in order to be accessible by ViewController Bridging

```swift
ViewState<SuccessState, ErrorState, LoadingState, EmptyState>
```


