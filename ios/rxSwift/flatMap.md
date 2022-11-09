# FlatMap


Think of it as an 2D array flat mapping into a 1D array


# Traditional
Flat Map 2D => 1D Array of Int values

```
[ 
	1,2,3,
  4,5,6,
  7,8,9
]                    ====> [1,2,3,4,5,6,7,8,9] 

```



## Reactive

// Imagine the variables as observable without the appropriate syntax.

```swift

let Observable1<[Int]> = [1,2,5]
let Observable2<[Int]> = [4,7,5]
let Observable3<[Int]> = [3,9,7]


[ 
	Observable1<[Int]>,
	Observable2<[Int]>,
	Observable3<[Int]>,
]

// Reaches into the observable of array of Int & unfurls itself
// Observable needs to be completed to unfurl. 

====> 
[ 1, 2, 5, // (Observable1.onComplete())
	4, 7, 5, // (Observable1.onComplete())
	3, 9, 7  // (Observable1.onComplete())
]

```


Inner observable -> completes of 1 out of 3 
It will wait for all 3 observables to complete their observable chain.
Flat maps are easier to discern if we one offs observable.of() or observable.just() which only processes one element and sends .onNext(value) => .onComplete(_) event to end its observable chain.



https://betterprogramming.pub/rxswift-deep-inside-flatmap-1ca150c41b18?gi=5416d91e4282


https://stackoverflow.com/questions/49361386/rxswift-wait-for-observable-to-complete



## Error Observable < T.success, T.failure >

Error
```text
 Declared closure result 'Observable<Result<User, Error>>' is incompatible with contextual type 'Result<T, Error>'
 Generic parameter 'T' could not be inferred
```

```swift
let userEmpty = authenticationSubject
	// This following code causes aforementioned compilation error
	.map { auth -> Observable<Result<User, Error>> in
		UserCoordinator().rx.currentUser(in: nil)
	}
```

This fixes it, don't fully understand it why but it could be related to unwrapping its internal observable sequence or else it would be `Observable<Observable<Result<User, Error>>>`

```swift
let userEmpty = authenticationSubject
   .flatMapLatest { auth -> Observable<Result<User, Error>> in
		UserCoordinator().rx.currentUser(in: nil)                 }
```