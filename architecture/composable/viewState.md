
A generic enumeration that wraps the state types in a simple enum case
```swift
public enum ViewState<F: ViewSuccess, E: ViewErrable, L: ViewLoadable, O: ViewEmptiable>: ViewStateProtocol {

    case success(F)
    case error(E)
    case loading(L)
    case empty(O)

    public var success: F? {
        guard case ViewState.success(let state) = self else { return nil }
        return state
    }

    public var error: E? {
        guard case ViewState.error(let state) = self else { return nil }
        return state
    }

    public var loading: L? {
        guard case ViewState.loading(let state) = self else { return nil }
        return state
    }

    public var empty: O? {
        guard case ViewState.empty(let state) = self else { return nil }
        return state
    }

}
```
