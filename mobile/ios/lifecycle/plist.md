# Plist

## Read App version

This will get the app version from Info.plist so that you could display it in the App settings.

```swift
guard let appVersion = Bundle.main.infoDictionary?["CFBundleShortVersionString"] as? String else { return }

guard let buildNumber = Bundle.main.infoDictionary?["CFBundleVersion"] as? String else { return }
```

