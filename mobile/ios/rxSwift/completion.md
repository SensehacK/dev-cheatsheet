

# Completion

## Introduction

So when you want to send completion events for your observable chain in order to signal the consumers or observers that its time to wrap up.

But side note I have also observed that sometimes listening to `onComplete` events on `.subscribe{}` & `.bind(to:)` has sometimes disposed the event early and which leads to getting an `.completed` event from the RxObservable chain.


## Model 


```swift

public class Custom { } // Model

public protocol CustomViewModelProtocol {

    var input: CustomViewModel.Input { get }

    var output: CustomViewModel.Output { get }

}
```
## ViewModel

Defining its appropriate initial states and sending observable event with specific type `.Completion` which would signal the observers / consumers of this ViewModel to do something after they receive specific event type.

```swift

public class CustomViewModel: ViewModellable {

	public typealias ViewStateType = ViewState<CustomState, DisplayableError, LoadingState, CustomStateEmptyState>
	
	let initialState = CustomState(param1: Type)
	 
	let initialViewState = ViewStateType.fulfilled(initialState)
	     
	let viewStateSubject = BehaviorSubject<ViewStateType>(value: initialViewState)
	
	let customContext = BehaviorSubject<Custom>(value: Custom())
	
	customContext
		.mapToVoid()
		.subscribe(onNext: viewStateSubject.onCompleted)
		.disposed(by: disposeBag)
}
            
```


## ViewController



```swift

class CustomViewController: UIViewController, ViewStateResponsive {

	private let viewModel: CustomViewModelProtocol
	
	var viewState: Driver<CustomViewModel.ViewStateType> { viewModel.output.viewState }

	viewState
		.asObservable()
		.debug("Completed viewState")
		.subscribe(onCompleted: { [weak self] in
			self?.dismiss(animated: true)
		})
		.disposed(by: disposeBag)
}

```


Listening to the ViewModel while adhering to the ViewState architecture and having Input & Output as structs for easy I/O from `Model = = ViewModel = = ViewController` 
