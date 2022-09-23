
## Code block interval

When you want to run a specific block of code every interval you can create an interval which fires off that Rx chain every time interval


```swift
let tempValue: String = "Kautilya"
let isStatusValid = Observable<Int>
	.interval(.seconds(Constant.refreshTokenInterval),
	 scheduler: MainScheduler.instance)
	 .mapToVoid()
	 .map { tempValue in 
		let result1 = doSomething()
		let result2 = doSomethingExtra()
		return result1 || result2 
	 }
	 .mapToVoid()
	 .share()



isStatusValid
	.subscribe(onNext: { status in 
		status ? doSomethingValid() : doSomethingInvalid()
	})
	.disposed(by: disposeBag)

```