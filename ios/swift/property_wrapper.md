# Property Wrapper

## Intro

Use to implicitly wrap values around elements to set some default initializer or configuration. This avoids adding more boilerplate code towards the codebase as well as reads really nice.
Swift UI has lots of property_wrappers and you can achieve so many of those functionality in this way with UIKit & Storyboard frameworks.

## Extension

### AutoLayout 
Property Wrapper for UIView - auto layout default setup.
Only downside is it cannot work with `lazy` variables

```swift
import UIKit

@propertyWrapper
public struct AutoLayout<T: UIView> {
  public var wrappedValue: T {
	didSet {
	 wrappedValue.translatesAutoresizingMaskIntoConstraints = false
	}
}

  public init(wrappedValue: T) {
	wrappedValue.translatesAutoresizingMaskIntoConstraints = false
	self.wrappedValue = wrappedValue
	}
}
```


## Trimmed

```swift
@propertyWrapper
public struct Trimmed {
    var value: String

    public init(wrappedValue: String) {
        self.value = wrappedValue
    }

    public var wrappedValue: String {
        get {
            value.trimmingCharacters(in: .whitespacesAndNewlines)
        }
        set {
            value = newValue
        }
    }
}
```

User Defaults Property Wrapper
[codable](codable.md)


## links

https://www.toptal.com/swift/wrappers-swift-properties

https://swiftwithmajid.com/2021/08/11/how-to-create-a-property-wrapper-in-swift/

https://quickbirdstudios.com/blog/swift-property-wrappers/