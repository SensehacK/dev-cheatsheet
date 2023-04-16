## MVVM

[MVVM](MVVM.md)
Model View ViewModel

Doesn't define how VM communicates with VC and Model layer.
You can use Functional Reactive programming, KVO pattern, Closures, Delegate pattern

Swift UI embeds this thorougly.
Data Flow.
View controler  < - > View Model < - > Model

VM -> Speaks to View Controller.
VM -> Speaks to Model

Pros:
- VM - Business logic is seperate

- Easily testable
- Dependency Injection  | Seperation of Concerns
-  SOLID principles
- Promotes Reusuability accross diff platforms iOS, iPadOS, MacOS, WatchOS, Catalyst.
- Great with Reactive paradigm

Cons:
- View Controller still has bloated code.
- 




