So a ViewModel in order for ViewController to consume these things needs to conform to this protocols.

```swift
protocol CustomViewModelProtocol {
    var input: CustomViewModel.Input { get }
    var output: CustomViewModel.Output { get }
}

class CustomViewModel: ViewModellable {
	typealias ViewStateType = ViewState<CustomState, CustomErrorState, CustomLoadingState, Never>
	// Properties
	let input: Input
	let output: Output
}
```



## Input Output

You're conforming to the `CustomViewModelProtocol` in an extension. This is the bridging in a way where ViewControllers would hold a reference of `ViewModel` and it would be able directly pass data and retrieve data via this protocol conformance with two different structs `Input` and `Output`.

```swift
extension CustomViewModel {
    public struct Input {
	    let loginAction: AnyObserver<Void>
	    let refreshToken: AnyObserver<String>
	    
    }
    
    public struct Output: ViewStateDrivable {
	    let viewState: Driver<ViewStateType>
    }
}
```

You can find those details of `ViewState<F: ViewSuccess, E: ViewErrable, L: ViewLoadable, O: ViewEmptiable` conformance by either resorting to `Memberless structs` defined in [viewStateProtocol](viewStateProtocol.md) or you can create your own model states by conforming to these protocols. You can find custom model state conformance in file [viewStateCustomModel](viewStateCustomModel.md)


```swift
extension CustomViewModel: ViewModelType {
    public struct Input {
	    let loginAction: AnyObserver<Void>
	    
    }
    
    public struct Output: ViewStateDrivable {
	    let viewState: AnyObserver<String>
    }
}

protocol ViewModelType {
    associatedtype Input
    associatedtype Output
    
    var input: Input { get }
    var output: Output { get }
}
```

