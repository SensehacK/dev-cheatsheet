# Localization

## Extension

Using Extension String

```swift
import Foundation

extension String {
    var localStr: String {
        return NSLocalizedString(self, comment: "")
    }
}
```

## Strings File

Define file Localizable.strings

```text
/* 
  Localizable.strings
*/

// MARK: - Navigation
"home.name.placeholder" = "Sense";
"home.data.info" = "My Data";
"home.user.name" = "Kautilya";
"browse.data.info" = "Browse Data";
"settings.info" = "Open Settings";
"settings.ui.mode" = "Choose UI Mode";
"settings.team.name" = "Our Core Team";
```

## Access

Accessing the strings from localized datastore, so it is overall cleaned approach with how getter works with strings without adding extra bloat or verbose code.

```swift
home.title.text = Texts.title.rawValue.localized,
home.username.text = Texts.user.rawValue.localized,
```

## Enums

Use enums to avoid long string access, and these enums would be limited to specific files of classes. Like this enum would be defined in specifically for specific class “home”. Home -&gt; Texts -&gt; Title

```swift
private enum Texts: String {
        case title = "home.name.placeholder"
        case user = "home.user.name"
    case description = "authorization.required.description"
    case cancel = "authorization.required.cancel"
    case confirm = "authorization.required.confirm"

}
```

