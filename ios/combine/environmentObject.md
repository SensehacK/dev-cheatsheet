
## Syntax

Before @Observable & `import Observation`

```swift
SettingsView()
	.environmentObject(appSettings)

struct SettingsView: View {
  @EnvironmentObject var appSettings: AppSettings
}
```

Now

```swift
SettingsView()
	.environment(appSettings)

struct SettingsView: View {
  @Environment(AppSettings.self) var appSettings
}
```


## Binding to an Environment Object

New changes makes it now easier

```swift
struct SettingsView: View {
  @Environment(AppSettings.self) var appSettings
  
  var body: some View {
    // Create a bindable appSettings
    @Bindable var appSettings = appSettings

    Toggle("Confirm deletion",
           isOn: $appSettings.confirmDeletion)
  }
}
```




