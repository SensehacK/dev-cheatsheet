
The idea behind this is to have protocols define certain variables available for any model who needs to have easier `Input & Output` definition in general.


## Input
```swift
public protocol ViewModelInput {
    associatedtype Input
    var input: Input { get }
}
```

## Output

```swift
public protocol ViewStateDrivable {
    associatedtype ViewStateType: ViewStateProtocol
    var viewState: Driver<ViewStateType> { get }
}

public protocol ViewModelOutput {
    associatedtype Output: ViewStateDrivable
    var output: Output { get }
}
```

## Combined Protocol Conformance

```swift
public typealias ViewModellable = ViewModelInput & ViewModelOutput
```

So here this typealias will be nicer way to represent conformance of both Input and Output protocols respectively. This protocol needs to consumed by `ViewModel` layer who is trying to follow the two way binding of data processing. Or making a `open close` principle of how data gets passed through these interfaces.

We are basically defining a contract between 
```
Input
view controller (publisher) <==> view model (consumer) 

Output
view model (publisher)  <==>  view controller (consumer)
```
This is how the Data flow should be happening in normal circumstances.



