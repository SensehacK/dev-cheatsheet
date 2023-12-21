
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

## Mind Map

RxSwift equivalent [combination](combination.md)

## References

[Merging Publishers With Combine's Merge Operator](https://cocoacasts.com/combine-essentials-merging-publishers-with-combine-merge-operator)

