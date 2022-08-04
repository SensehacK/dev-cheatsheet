# Bind vs Subscribe

LoginViewModel Ln: 251


```swift

  .bind(to: dashboardNavigationContextSubject)
            
  vs
            
	.subscribe(onNext: { data in
                dashboardNavigationContextSubject.onNext(data)
```