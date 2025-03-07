

## Thermal State

```swift
NotificationCenter
    .Publisher(center: .default,
	    name: ProcessInfo.thermalStateDidChangeNotification)
    .sink { [weak self] (notification) in
		self?.responseToHeat(notification)
	}
	.store(in: &cancelBag)

@objc 
private func responseToHeat(_ notification: Notification ) {
    let state = ProcessInfo.processInfo.thermalState
    switch state {
    case .nominal:
      DDLogInfo("THERMAL: Thermal state is nominal (0).  No action needed.")
    case .fair:
      DDLogInfo("THERMAL: Thermal state is fair (1).  Device is starting to heat up. Reduce expensive CPU operations.")
    case .serious:
      DDLogInfo("THERMAL: Thermal state is SERIOUS (2).  Time to reduce CPU usage and device charging.")
    case .critical:
      DDLogInfo("THERMAL: Thermal state is CRITICAL (3).  Cool down the device NOW.")
    @unknown default:
      DDLogInfo("THERMAL: Thermal state is UNKNOWN.")
    }
  }
```

[SO | thermal state monitoring Singleton](https://stackoverflow.com/a/70139834/5177704)