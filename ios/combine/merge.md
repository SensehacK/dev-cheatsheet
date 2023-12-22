
# Merge

## Syntax

```swift
let mediaChange = NotificationCenter
    .default
    .publisher(for: AVPlayerItem.mediaSelectionDidChangeNotification)
    .dropFirst()
    .map { _ in }
    .eraseToAnyPublisher()
        
let mediaReady = avPlayer
	.publisher(for: \.timeControlStatus)
	.filter({ $0 == .playing })
	.map { _ in }
	.eraseToAnyPublisher()

Publishers
	.Merge(mediaChange, mediaReady)
	.sink { [weak self] _ in
		self?.trigger()
	}
	.store(in: &cancellables)

```

## N - Merge

The **Combine** framework also defines several variants of the `Merge` struct that support merging more than two publishers, `Merge2`, `Merge3`, `Merge4`, `Merge5`, `Merge6`

```swift
private func setupBindings() {
    let willEnterForeground = NotificationCenter.default.publisher(for: UIApplication.willEnterForegroundNotification, object: nil)
    let didEnterBackground = NotificationCenter.default.publisher(for: UIApplication.didEnterBackgroundNotification, object: nil)
    let didBecomeActive = NotificationCenter.default.publisher(for: UIApplication.didBecomeActiveNotification, object: nil)
    let willTerminate = NotificationCenter.default.publisher(for: UIApplication.willTerminateNotification, object: nil)

    Publishers
    .Merge4(
    willEnterForeground,
    didEnterBackground,
    didBecomeActive,
    willTerminate)
    .sink(receiveValue: { [weak self] _ in
		self?.doSomething()
	}).store(in: &subscriptions)
}
```

## Mind Map

RxSwift equivalent [combination](combination.md)



## References

[Apple dev | combine merge](<https://developer.apple.com/documentation/combine/fail/merge(with:_:)>)

[Merging Publishers With Combine's Merge Operator](https://cocoacasts.com/combine-essentials-merging-publishers-with-combine-merge-operator)

