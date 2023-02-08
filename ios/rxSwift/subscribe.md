

## Introduction

Subscription is the basis of any Observable being observed by its observers.
You need to subscribe in order to tap into the stream of events the observable is passing to its subscribers. 




## Normal Subscribe

We have observable which can pass events where any of the three types of events could be passed.
Event
✅ - Completed
❌ - Error
💰 - Value

```swift

let first_observable = Observable<String>.create { observer in
	// 1
	observer.onNext("1")
	// 2
	observer.onCompleted()
	// 3
	observer.onNext("?")
	// 4
	return Disposables.create()
}

first_observable
	.subscribe{ (event) in
		switch event {
		case .next(let value):
			print("💰 Value: \(value)")
		case .completed:
			print("✅")
		case .error(let error):
			print("❌ \(error)")
		}
	}

}

```

###  Notice

// 3 Doesn't get transmitted because once an observable gets `.complete()` event sent then it terminates the stream. So be very careful with `.complete` events.


## Just subscribe

Sometimes you don't need to fully complete the completion handler with closures et & you just need to quickly subscribe to it so that you can inspect the map of the data being passed around the stream.


```swift

// Observable
func fetchData() -> Single<Data_Model> { 
	
	return Single.create { (single) -> Disposable in
	
		if random_number > 10 {
			return Single(.success(Data_Model))
		} else {
			return Single(.failure(Custom_Error.myError))
		}
}



// Observer // Subscriber
fetchData()
.map { data_model in 
	print(data_model.custom_property)
}
.subscribe() // This can be empty in order to initialize
.disposed(by: disposeBag)


```


## Quirks

### Opening parathesis Matters

Just noticed this small quirk in playground that if my `(` is on the next line it won't compile properly for subscribe block

Doesn't work
```swift
observable
	.subscribe
(
	onNext: { }
)
```
Works
```swift
observable
	.subscribe(
	onNext: { }
)


