

## System Memory

Tracking those states

```swift

private let systemMemory = SystemMemory()

func setupMemoryWarningBindings() {
	UIApplication.rx.didReceiveMemoryWarning
        .withUnretained(systemMemory)
        .subscribe(onNext: { systemMemory, _ in
           CacheManager.shared.persistOfflineCache()
                AppLogger.event(event: AnalyticEvent.Errors.lowMemoryWarning.userActionEvent)

            })

            .disposed(by: disposeBag)

    }


class SystemMemory {
					
}
```
## Firebase
[firebase](firebase.md)

## Dynamic Symbols

[dSYM](dSYM.md)


##