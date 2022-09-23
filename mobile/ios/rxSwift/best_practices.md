# RxSwift Best Practises

Listing overall learnings of RxSwift do's and don'ts for writing good reactive code which is easily discernible and succinct enough to get the job done.


## Code structure

### Input & Output

We use structs inside our classe
s with explicit definition called "Input" and "Output"

Eg.
```swift

extension AnyViewModel {
    public struct Input {
        public let newAppName: AnyObserver<String>
        public let currentAppSelection: AnyObserver<App>
        public let navigateAppsList: AnyObserver<Void>
    }
    
    public struct Output {
        public let navigationContext: Driver<NavigationContext>
        public let dismiss: Driver<Void>
    }
}

```


### ViewState Architecture

We also have ViewState Architecture which gets subscribed from Rx point of view to have uninterrupted view state updates. Conformance to protocol `ViewStateDrivable` is required.

```swift
extension AnyViewModel {
	
	public struct Output: ViewStateDrivable {
	        public let viewState: Driver<ViewState<AppSelectionState, Never, Never, Never>>
	        public let navigationContext: Driver<NavigationContext>
	    }

}
```


## Syntactic Sugar

Where writing less and concise is the way of life 😌

### Unretained Self
When referencing self in a closure like we always want to have weak reference in order to avoid retaining the reference thus creating a retain cycle which won't be released automatically by ARC (Automatic Reference Counting) mechanism.

Example

Old way
```swift
let closeButtonItem = UIBarButtonItem(.close)
closeButtonItem
    .rx
    .tap
    .asObservable()
    .subscribe(onNext: { [weak self], _ in
        self?.dismiss(animated: true)
    })
    .disposed(by: self.disposeBag)
```


New Way
```swift
let closeButtonItem = UIBarButtonItem(.close)
closeButtonItem
    .rx
    .tap
    .asObservable()
    .withUnretained(self)
    .subscribe(onNext: { owner, _ in
        owner.dismiss(animated: true)
    })
    .disposed(by: self.disposeBag)
```



### Unwrapping in chain

You may sometimes get an optional value as a return type and it is not that good looking when reading the code where there is optional binding involved in that Rx Chain.
Luckily to make the code more readable you could extend Rx to provide us some utilities which does the unwrapping for us.


Old Code: Though I'm not sure guard else statement in RxCocoa eg. would suffice empty `FormFieldState()` object.

```swift
tableView
    .rx
    .itemDeleted
    .asObservable()
    .map { [weak dataSource] indexPath in
        guard let formField = dataSource?[indexPath] else { return FormFieldState() } // Optional unwrap
        return formField
    }
    .bind(to: viewModel.input.deleteFormField)
    .disposed(by: disposeBag)
```

New Code
```swift
tableView
    .rx
    .itemDeleted
    .asObservable()
    .map { [weak dataSource] indexPath in
        return dataSource?[indexPath]
    }
    .unwrap()
    .bind(to: viewModel.input.deleteFormField)
    .disposed(by: disposeBag)
```

Extension code
```swift
extension ObservableType where Element: ExpressibleByNilLiteral {
    /// Unwraps an observable and emits the value of a non nil value to the Rx stream, or stops the stream if the value is nil.
    public func unwrap<T>() -> Observable<T> where Element == T? {
        return flatMap { Observable.from(optional: $0) }
    }
}
```


## Right tool

Choosing the right tool is always the hardest job one might argue. Should we go for merge or flatMapLatest or just flatMap. Rx provides lots of tools under its belt and it can be overwhelming sometimes to pick one tool over another.

### UI

For UI elements always go for Rx Traits as they are basically Subjects but they don't error out.

Relays are a good example as they are ran on main thread so that the UI work is performed on highest priority and would not have undesirable side effect from it.


## View Model

I'm not 100% sure but I believe we extensively use Subjects in our ViewModel with structure of "Input" and "Output" to further differentiate who does what and its expectations.




