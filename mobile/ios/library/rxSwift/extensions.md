# Extensions

Things to make your Rx life easier



Unwrap optionals in Rx


```swift
import RxSwift

extension ObservableType where Element: ExpressibleByNilLiteral {
    /// Unwraps an observable and emits the value of a non nil value to the Rx stream, or stops the stream if the value is nil.
    public func unwrap<T>() -> Observable<T> where Element == T? {
        return flatMap { Observable.from(optional: $0) }
    }
}

public extension ObservableType where Element: ExpressibleByNilLiteral {
    func unwrap<T>(default defaultWhenNil: T? = nil) -> Observable<T> where Element == T? {
        return self.flatMap { Observable.from(optional: $0 != nil ? $0 : defaultWhenNil) }
    }
}

public extension ObservableType where Element == Optional<Bool> {
    /// Unwraps the observable and emits any non `nil` value to the Rx stream, or emits the supplied `defaultWhenNil` argument if the value is `nil`.
    ///
    /// The default value of `defaultWhenNil` is `false`.
    func unwrap(default defaultWhenNil: Bool = false) -> Observable<Bool> {
        return self.map { $0 ?? defaultWhenNil }
    }
}
```

## Debug Helper

```swift

public extension ObservableType {
    /**
     Trimmed console output on Observables.
     */
    func debugShort(_ identifier: String? = nil) -> Observable<Element> {
        return debug(identifier, trimOutput: true)
    }
}

```


## Mapping Observable

```swift

		/// Maps any Observable types to a void.
    func mapToVoid() -> Observable<Void> {
        return map { _ in }
    }

		/// Maps any Observable types to false.
    func mapToFalse() -> Observable<Bool> {
        return map { _ in false }
    }
    
    /// Maps any Observable types to true.
    func mapToTrue() -> Observable<Bool> {
        return map { _ in true }
    }
    
    /// Maps any Observable types to an optional Any.
    func mapToAny() -> Observable<Any?> {
        return map { $0 as Any? }
    }
    
    /// Maps any Observable type to `Optional<T>.none`, coercing the source sequence into optional type T result sequence.
    func mapToNil<T>(_ type: T.Type) -> Observable<T?> {
        return map { _ in nil }
    }
```

## Observable to Result

```swift
extension ObservableType {
    /// Returns the Result object of either success or failure.
    public func toResult() -> Observable<Result<Element, Error>> {
        return map { .success($0) }
            .catch { .of(.failure($0)) }
    }
}
```

## Result ObservableType

```swift

public extension ObservableType where Element: ResultType {
    /// Unwraps the value from a Result, or stops the stream if the value is nil.
    func unwrapSuccess<T>() -> Observable<T> where Element == Result<T, Error> {
        return map { $0.value }.unwrap()
    }
    
    /// Unwraps the error from a Result, or stops the stream if the error is nil.
    func unwrapFailure<T>() -> Observable<Error> where Element == Result<T, Error> {
        return map { $0.error }.unwrap()
    }
    
    func unwrapSuccessFailure<T>() -> (success: Observable<T>, failure: Observable<Error>) where Element == Result<T, Error> {
        let sharedSelf = self.share()
        return (sharedSelf.unwrapSuccess(), sharedSelf.unwrapFailure())
    }
}

public protocol ResultType {}

extension Result: ResultType {}


```


## Extenisfying Everything

My comment on recent extension addition towards ControlEvents across iOS UI life cycle events.

[Gitlab MR comment](https://gitlab.com/xvia/mobile/TrackVia-iOS/-/merge_requests/1129#note_938251301)