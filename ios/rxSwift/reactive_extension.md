# Swift Reactive extension







## Creating Observable with Result type. 
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