


## Initialize


```swift
private var customDisposeBag = DisposeBag()

```


## Deinitialize


```swift
private var customDisposeBag = DisposeBag()

let customObservable = Observable.of([1,4,5])

customObservable
	.subscribe(onNext { asd in 
		print(asd)
		return true
	})
	.disposed(by: customDisposeBag)


// Stop tracking by simply disposing the bindings
customDisposeBag = .init()
        
```