
## Setup

```swift
class CustomViewController: UIViewController, ViewStateBridger {
    private let viewModel: CustomViewModelProtocol
    var viewState: Driver<CustomViewModel.ViewStateType> { viewModel.output.viewState }

```

## Usage


```swift

class CustomViewController {
	let disposeBag = DisposeBag()
	
	init() { 
		setupListeners()
	}

	func setupListeners() {
		success
            .map(\.canRequestNetwork)
            .bind(to: )
            .disposed(by: disposeBag)

		loading
            .mapToVoid()
            .showAlert(text: "Calm down mkay! I'm loading.",
                         context: Context(.caseOne))
            .disposed(by: disposeBag)

		error
            .map(\.displayableError)
            .unwrap()
            .showErrorAlert(text: "You ducked! up")
            .disposed(by: disposeBag)
	}
}
```