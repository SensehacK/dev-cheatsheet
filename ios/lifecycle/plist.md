# Plist

## Read App version

This will get the app version from Info.plist so that you could display it in the App settings.

```swift
guard let appVersion = Bundle.main.infoDictionary?["CFBundleShortVersionString"] as? String else { return }

guard let buildNumber = Bundle.main.infoDictionary?["CFBundleVersion"] as? String else { return }
```


## Privacy Descriptions

Anything related to privacy, apple asks us to explicitly ask for permission to the user by stating that permission description in `Info.plist`


- Location access
- Camera usage
- Bluetooth usage



## Network Security

URL  App Transport Security Plist explicit descriptions
[ats_plist](ats_plist.md)
[security](security.md)


## No Storyboard

[No main storyboard](/ios/lifecycle/view_controllers#No Storyboard Xcode)



## App Info 

Build number
[auto_increment](auto_increment.md)


## Orientation

[orientation supported](orientation.md)

## Keys

[secret_keys](secret_keys.md)



