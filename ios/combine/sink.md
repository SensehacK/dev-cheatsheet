
## Intro

Sink is the equivalent of `subscribe` of RxSwift with Swift Combine.

RxSwift reference
[subscribe](subscribe.md)

## Usage

```swift
import Combine

class QuotesViewModel: ObservableObject {

    private var cancellables = Set<AnyCancellable>()
    @Published var quotes = [Quote]()

    func getQuotesData() {
        AsyncNetwork.shared.fetchData(url: Constants.quotesAPIURL, type: String.self)
            .sink { completion in
                switch completion {
                case .failure(let error): print(error)
                case .finished: print("Finish")
                }
            }
            receiveValue: { self.quotes = $0.quotes }
            .store(in: &cancellables)
        }
}
```
## Two Parameters

This thing could be tied down with RxSwift `subscribe` block returning `Event<Type` of `.Complete`, `.Error` & `Next<Value>`
Reference of RxSwift completion [completion](completion.md)
### Completion


### Receive Value



## quirks

In one scenario I had to assign the value of async await to the published value of the class. 
The code which is in question is `self.customVM = ` .
Probably dealing around AnyCancellable - RxSwift Disposable kind of memory management retention.


```swift
class LocationManager { 
	 @Published var location: CLLocationCoordinate2D?
}

class customVM: ObservableObject {
	@Published var customVM: CustomVM?
	private var anyCancellables = Set<AnyCancellable>()

locationManager.
	$locations
	.asyncMap { location -> CustomModel? in 
		self.customVM = CustomViewModel(city: weatherCity)
		// Create object or nil
		return nil
	}
	.receive(on: DispatchQueue.main)
	.sink { _ in }
	.store(in: &anyCancellables)
}
```


Or just use 
```swift
.assign(to: &$weatherVM)
```

By switching to assign, I believe apple takes care of retaining that subscription till the time the main class is kept  in memory and someone is holding that reference of the class.
