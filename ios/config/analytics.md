# Analytics

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
class SystemMemory { }
```

## Firebase
[firebase](firebase.md)

### app measurements

[SO | firebase app measurement](https://stackoverflow.com/questions/54461349/how-to-decrypt-firebase-requests-to-app-measurement-com/54463682#54463682)

## Dynamic Symbols

[dSYM](dSYM.md)

