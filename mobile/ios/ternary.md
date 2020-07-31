# Ternary

## Conditional

True false situation checker.

## Toggle states

```swift
// MARK: - Types
    enum Content {

        case case1
        case case2

        /// Toggles between content
        mutating func toggle() {
            self = self == .case1 ? .case2 : .case1
        }

    }

    // MARK: - Observed Properties
    private var content: Content = .case1 {
        didSet {
            contentDidChange()
        }
    }

    // MARK: - Calling the func from enum
    content.toggle()
```

