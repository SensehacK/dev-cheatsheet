

## System namespace

Overriding the system namespace which are reserved could be avoided using backticks

```swift
public enum Bool {

        public static let `false` = "false".localized

        public static let `true` = "true".localized

    }
```
