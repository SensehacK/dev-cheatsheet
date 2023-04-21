

RxSwift Reactive extensions for eliminating the same boilerplate code.


## Observable Type
```swift
extension ObservableType where Element: ViewStateProtocol {

    var success: Observable<Element.FulfilledType> {
        return self.map { $0.success }.unwrap()
    }

    var error: Observable<Element.ErrorType> {
        return self.map { $0.error }.unwrap()
    }

    var loading: Observable<Element.LoadingType> {
        return self.map { $0.loading }.unwrap()
    }

    var empty: Observable<Element.EmptyType> {
        return self.map { $0.empty }.unwrap()
    }
}
```


## Driver Type

```swift
public extension Driver {
    func unwrap<T>() -> Driver<T> where Element == T? {
        return self.flatMap { Driver.from(optional: $0) }
    }
}

public extension Driver where Element: ViewStateProtocol {
    var success: Driver<Element.SuccessType> {
        return self.map { $0.success }.unwrap()
    }
    
    var error: Driver<Element.ErrorType> {
        return self.map { $0.error }.unwrap()
    }
    
    var loading: Driver<Element.LoadingType> {
        return self.map { $0.loading }.unwrap()
    }

    var empty: Driver<Element.EmptyType> {
        return self.map { $0.empty }.unwrap()
    }
}
```

## Usage

###  Observable Type 

```swift
let viewState = customViewModel
	.output
	.viewState
	.asObservable()

viewState
	.success
	.map(\.items)
	.bind(to: customViewModel.appListItemsObserver)
	.disposed(by: disposeBag)
```

### Driver Type

```swift
fulfilled
	.map(\.tokenExpire)
	.subscribe(onNext: { [weak customView] isVisible in
		customView?.setButtonVisibility(visible: isVisible)
	})
	.disposed(by: disposeBag)

error
	.mapToTrue()
	.bind(to: customView.isInputVisible)
	.disposed(by: disposeBag)
```
We get `\.tokenExpire` from `ViewStateCustomModel` file in which we have custom model `CustomState: ViewSuccess` conformance which in relation the extension of `Driver where Element: ViewStateProtocol`  allows us to unwrap internally.

## Syntactic Sugar

Extra helper methods for syntactic sugar around these things.

```swift
public extension ViewState {
    var isLoading: Bool {
        return self.loading != nil
    }
    var isNotLoading: Bool {
        return !isLoading
    }
    var isNotEmpty: Bool {
        return self.empty == nil
    }
    var isError: Bool {
        return self.error != nil
    }
}
