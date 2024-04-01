
## Mind Map

RxSwift equivalents [[Observe]]

[[concurrency_rxSwift]]

## Code

added this to the sink configuration

```swift
private let viewModel = LoginVM ()

viewModel
.userPub
.receive (on: DispatchQueue.main)  
.sink { user in 
	print ("The thread: \(Thread.current) with user \(user)")
}

viewModel.fetchUser()

struct LoginVM {
	private let userSub = PassthroughSubject<User, Never> ()
	
	var userPub: AnyPublisher<User, Never> { userSub.eraseToAnyPublisher() }

	func fetchUser() {
		DispatchQueue
		.global()
		.async {
			print ("The SEND thread: \ (Thread. current)")
			userSubject.send(User())
		}
	}
}

```



```swift
.receive(on: DispatchQueue.main)
.receive(on: DispatchQueue.global)
.receive(on: RunLoop.main)
```

## Tips

Now let’s gather all the data we collected until now into some advice:

- Be mindful of which thread you will run your sink closures. If you don’t define the default `Scheduler` will be used and it’s based on where the data is created.
- Never rely on the default `Scheduler` to run your code if it changes UI.
- A good pattern for your async code is to **subscribe in the background thread and receive on the main thread**.

## Subscribe(on: )


```swift
.subscribe(on: DispatchQueue.global())
.subscribe(on: DispatchQueue.main))
.subscribe(on: RunLoop.main)

```

## Resources

Code snippet and tips from this article below
[Swift and Combine: Which thread runs my sink closure?](https://holyswift.app/swift-and-combine-which-thread-runs-my-sink-closure/)

[Apple dev | Receiving and Handling Events with Combine](https://developer.apple.com/documentation/combine/receiving-and-handling-events-with-combine) 