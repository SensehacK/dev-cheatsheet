Subscription Chain not firing

```
let accounts = (0...4)
            .map { value in
                Account(id: value, accountFeatures: [], accountTheme: nil, createdAt: nil, databaseName: nil, domain: nil, packageName: nil, sandboxName: nil, sessionTimeout: nil, subDomain: nil, updatedAt: nil)
            }
            .map(AccountState.init)

Observable.
		        of(accounts)
            .map(AccountInfoState.init)
            .map(ViewStateType.fulfilled)
            .bind(to: viewStateSubject)
            .disposed(by: disposeBag) 
            
```


```swift
        Observable
            .create { observer in
                let accounts = (0...4)
                    .map { value in
                        Account(id: value, accountFeatures: [], accountTheme: nil, createdAt: nil, databaseName: nil, domain: nil, packageName: nil, sandboxName: nil, sessionTimeout: nil, subDomain: nil, updatedAt: nil)
                    }
                    .map(AccountState.init)
                observer.onNext(accounts)
                return Disposables.create()
            }
            .map(AccountInfoState.init)
            .map(ViewStateType.fulfilled)
            .bind(to: viewStateSubject)
            .disposed(by: disposeBag)
            

            
```

// Note: For some weird reason Observable.of() doesn't create the observable type and emits the `.next()` event in the Rx chain.

