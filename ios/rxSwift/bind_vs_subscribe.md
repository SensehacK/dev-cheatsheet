# Bind vs Subscribe

```swift

  .bind(to: dashboardNavigationContextSubject)
            
  vs
            
	.subscribe(onNext: { data in
                dashboardNavigationContextSubject.onNext(data)
```


https://www.thedroidsonroids.com/blog/rxswift-by-examples-2-observable-and-the-bind

Different ways to do this.
```swift
	.subscribe(onNext: { authentication.on(.next($0)) })
    .bind(to: authentication)
	.subscribe(onNext: { auth in
		authentication.onNext(auth)
	})
```



https://docs.rxswift.org/classes/publishsubject#/s:7RxSwift14PublishSubjectC2onyyAA5EventOyxGF

https://www.stepintoswift.com/rxswift-publishsubject

https://medium.com/macoclock/rxswift-subjects-e7037e686a91