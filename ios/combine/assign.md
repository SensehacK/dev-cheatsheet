# Assign

## Intro

Assign is the equivalent of `bind` of RxSwift with Swift Combine.
RxSwift reference
[bind_vs_subscribe](bind_vs_subscribe.md)

## Usage

### Model

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

### View

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

### ViewModel

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
   
[updating-ui-with-assignto on-in-combine](https://www.donnywals.com/updating-ui-with-assigntoon-in-combine/)

## Async Combine Interop

[swift by sundell | calling-async-functions-within-a-combine-pipeline](https://www.swiftbysundell.com/articles/calling-async-functions-within-a-combine-pipeline/)

[async-await-support-for-combines-sink-and-map](https://augmentedcode.io/2023/01/09/async-await-support-for-combines-sink-and-map/)

[combine-vs-async](https://peterfriese.dev/posts/combine-vs-async/)

## Binding 

### State and data flow

[Driving changes in your UI with state and bindings](https://developer.apple.com/tutorials/swiftui-concepts/driving-changes-in-your-ui-with-state-and-bindings)

[Combine’s What Makes SwiftUI Really Shine](https://infinum.com/blog/combine-makes-swiftui-shine/)

### onChange Event

```swift
struct ContentView: View {
    @State private var name = ""

    var body: some View {
        TextField("Enter your name", text: $name)
            .onChange(of: name) { oldValue, newValue in
                print("Changing from \(oldValue) to \(newValue)")
            }
    }
}
```

[hacking with swift | run code when state changes onChange](https://www.hackingwithswift.com/quick-start/swiftui/how-to-run-some-code-when-state-changes-using-onchange)
