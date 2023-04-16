

## Intro

Assign is the equivalent of `bind` of RxSwift with Swift Combine.
RxSwift reference
[bind_vs_subscribe](bind_vs_subscribe.md)


## Usage

Model
```swift
struct Quotes: Decodable {
    let quotes: [Quote]
    let total: Int
}
struct Quote: Identifiable, Decodable, Hashable {
    let id: Int
    let quote: String
    let author: String
}
struct Constants {
    static let quotesAPIURL = "https://dummyjson.com/quotes"
}
```
### SwiftUI
View
```swift
struct QuotesView: View {
    @ObservedObject var viewModel = QuotesViewModel()
    var body: some View {
        NavigationView {
            VStack {
                Text(viewModel.randomQuote)
                    
                VStack {
                    Button {
                        viewModel.getRandomQuote()
                    } label: {
                        Text("Get Random Quote")
                    }
                }
                .padding()
            }
            .navigationTitle("Random Quote")
        }
        .onAppear { viewModel.getQuote() }
    }
}
```

ViewModel
```swift
class QuotesViewModel: ObservableObject {
    private var cancellables = Set<AnyCancellable>()

    @Published var quotes = [Quote]()
    @Published var randomQuote: String = ""

    func getQuote() {
        AsyncNetwork.shared.fetchData(url: Constants.quotesAPIURL, type: Quotes.self)
            .sink { completion in
                switch completion {
                case .failure(let error): print(error)
                case .finished: print("Finish")
                }
            }
            receiveValue: { [weak self] quotesData in
                let quotes = quotesData.quotes
                self?.quotes = quotes
                getRandomQuote()
            }
            .store(in: &cancellables)
        }

    func getRandomQuote() {
        randomQuote = quotes.randomElement()?.quote ?? "No Random quote available"
    }

}
```


### UIKit

No need to do this way in Swift UI -> Just use `@Published` and SwiftUI is smart enough to figure out the subscriber / publisher model.

```swift
private let quotePub = PassthroughSubject<String, Never>()
var quoteAnyP: AnyPublisher<String, Never> {
	quotePub.eraseToAnyPublisher()
}
init() {
	quotePub.send("")
}
```
   

https://www.donnywals.com/updating-ui-with-assigntoon-in-combine/