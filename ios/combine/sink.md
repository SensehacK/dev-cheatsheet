


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




