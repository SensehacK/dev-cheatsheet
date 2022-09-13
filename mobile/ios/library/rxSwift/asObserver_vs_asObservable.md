AsObserver() vs AsObservable() 

AsObserver() 
First you can pass `.onNext(Events)` whoever has access.

Only access control would be granted access if they are in that authorized state.



```
otherAccountsSelected
            .debugLane("AccountList")
            .map { $0.account }
            .bind(to: context.switchAccount)
            .disposed(by: disposeBag)`
            
```

So bind -> Subscribe 

But can also bind data to pass the argument above to the observer's next event.

`.onNext event(Account)`


## Completion to Observable

https://stackoverflow.com/questions/50753875/rxswift-chain-completable-to-observable?rq=1