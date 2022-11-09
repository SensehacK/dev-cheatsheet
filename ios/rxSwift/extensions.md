# Extensions

Things to make your Rx life easier

## Extension Where

The where clause is  an important one to safely limit our extensions for specific types of elements. Which is also an optimization as well as limits undefined behavior with the wrong extension overload.

```swift
extension ObservableType where Element: ExpressibleByNilLiteral { }

extension ObservableType where Element == Optional<Bool> { }

extension ObservableType where Element: ResultType { }

extension Reactive where Base: UIViewController { }

extension ObservableType where Element == Void { }

```


## Optional Chaining

Unwrap optionals in Rx

```swift
import RxSwift

extension ObservableType where Element: ExpressibleByNilLiteral {
    /// Unwraps an observable and emits the value of a non nil value to the Rx stream, or stops the stream if the value is nil.
    public func unwrap<T>() -> Observable<T> where Element == T? {
        return flatMap { Observable.from(optional: $0) }
    }
}

extension ObservableType where Element: ExpressibleByNilLiteral {
    func unwrap<T>(default defaultWhenNil: T? = nil) -> Observable<T> where Element == T? {
        return self.flatMap { Observable.from(optional: $0 != nil ? $0 : defaultWhenNil) }
    }
}

extension ObservableType where Element == Optional<Bool> {
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

extension ObservableType {
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

extension ObservableType where Element: ResultType {
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


Creating Observable with Result type. 
Code example

```swift

public protocol RxAccountCoordinatorProtocol { }

public class AccountCoordinator: RxAccountCoordinatorProtocol { }

extension AccountCoordinator: ReactiveCompatible { }

extension Reactive: RxAccountCoordinatorProtocol where Base: AccountCoordinator {
    
    public func accountResult(accountGraph: Result<AccountGraph, Error> ) -> Observable<Result<Account, Error>> {
        
        return Observable.create { observer in
            
            observer.onNext(accountGraph.map(\.coreObject))
            
            // 2 .map can automatically open up new success block & still return previous error.
//            let result = accountGraph
//                .map { return $0.coreObject }
//            observer.onNext(result)

						// 1
//            switch accountGraph {
//            case .success(let accountGraph) :
//                observer.onNext(Result.success(accountGraph.coreObject))
//            case .failure(let error):
//                observer.onNext(Result.failure(error))
//            }

            return Disposables.create()
        }
    }
}



```


## Result Tuple

```swift
		/// Splits the observable sequence into two (2) separate observable sequences based on the condition block passed to this method.
    /// - Parameter condition: A block that returns a Bool value that determines how the sequence should be split.
    /// - Returns: A tuple whose first member is an observable sequence that met the condition and whose
    ///   second member is an observable sequence that didn't meet the specified condition.
    ///
    /// - NOTE: This method does not make any assumptions about shared resources, that is, it does not call `.share()` on the source observable before splitting it into two separate streams. It is up to the caller to determine if a `.share()` is needed and to call it accordingly. The `.share()` can be chained directly before calling this method.
		func split(_ condition: @escaping (Element) -> Bool) -> (wasTrue: Observable<Element>, wasFalse: Observable<Element>) {
        let wasTrue = self.filter(condition)
        let wasFalse = self.filter { !condition($0) }
        return (wasTrue, wasFalse)
    }


```

## Result Tuple Boolean
```swift

    func split() -> (wasTrue: Observable<Element>, wasFalse: Observable<Element>) where Element == Bool {
        let wasTrue = self.filter { $0 }
        let wasFalse = self.filter { !$0 }
        return (wasTrue, wasFalse)
    }
```



## UIViewController


```swift
import UIKit
import RxSwift
import RxCocoa

extension Reactive where Base: UIViewController {
    var viewDidLoad: ControlEvent<Void> {
        let source = self.methodInvoked(#selector(Base.viewDidLoad)).map { _ in }
        return ControlEvent(events: source)
      }

    var viewWillAppear: ControlEvent<Bool> {
        let source = self.methodInvoked(#selector(Base.viewWillAppear)).map { $0.first as? Bool ?? false }
        return ControlEvent(events: source)
      }

    /// ControlEvent that emits when the view controller's appearance state changes
    var isVisible: Observable<Bool> {
        let viewDidAppearObservable = self.base.rx.viewDidAppear.map { _ in true }
        let viewWillDisappearObservable = self.base.rx.viewWillDisappear.map { _ in false }
        return Observable<Bool>.merge(viewDidAppearObservable, viewWillDisappearObservable)
    }

    /// ControlEvent that emits when the ViewController is being dismissed.
    var isDismissing: ControlEvent<Bool> {
        let source = self.sentMessage(#selector(Base.dismiss)).map { $0.first as? Bool ?? false }
        return ControlEvent(events: source)
    }


}

```



My comment on recent extension addition towards ControlEvents across iOS UI life cycle events.

[Gitlab MR comment](https://gitlab.com/xvia/mobile/product_name-iOS/-/merge_requests/1129#note_938251301)


## Logging

```swift
extension ObservableType {

    func log(_ level: RxLog, lineNumber: Int = #line, function: String = #function) -> Observable<Element> {

        return self.do(onNext: { _ in

            Logger.log(level)

        })

    }

    func log(_ block: @escaping (Element) -> RxLogLevel?, lineNumber: Int = #line, function: String = #function) -> Observable<Element> {

        return self.do(onNext: { element in

            guard let level = block(element) else { return }

            Logger.log(level)

        })

    }

}

public enum RxLog {
	case warning(String)
    case error(String)
    case verbose(String)
    case fatal(String)
    case debug(String)
    case info(String)
}

```


## Subcribe

Overloading subscribe methods of `ObservableType` where Element is of type `Void`
```swift
extension ObservableType where Element == Void { }
```

    /// - NOTE: This is an method overload of `RxSwiftExt.subscribeNext<Object: AnyObject>
```swift
/// Subscribes an element handler to an observable sequence.
func subscribeNext<Object: AnyObject>(weak obj: Object, _ onNext: @escaping (Object) -> () -> ()) -> Disposable {
        return subscribe(onNext: { [weak obj] in
            guard let obj = obj else { return }
            onNext(obj)()
        })
    }
```