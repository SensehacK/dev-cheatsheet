# MVVM


## Intro

[MVVM](MVVM.md)
Model View ViewModel

Doesn't define how VM communicates with VC and Model layer.
You can use Functional Reactive programming, KVO pattern, Closures, Delegate pattern

Swift UI embeds this thoroughly.

## Data Flow

View controller  < - > View Model < - > Model

VM -> Speaks to View Controller.
VM -> Speaks to Model

## Pros
- VM - Business logic is separate
- Easily testable
- Dependency Injection  | Separation of Concerns
-  SOLID principles
- Promotes Reusability across diff platforms iOS, iPadOS, MacOS, WatchOS, Catalyst.
- Great with Reactive paradigm

## Cons
- View Controller still has bloated code.
- 


## Code Example

[MVVM_example_SwiftUI](MVVM_example.md)
## References

Dependency Injection
[singleton-dependency-injection-in-swift](https://getstream.io/blog/singleton-dependency-injection-in-swift/)

