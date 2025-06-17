# Extensions

Swift plays a great role in terms of extending current functionality in a clean code aspect and not cluttering the main class code implementation.

So with extensions you could just extend specific functionality to a specific class by just defining `extension className`


## Alerts

## Keyboard

[Keyboard Dismiss](https://stackoverflow.com/questions/11282449/move-uiview-up-when-the-keyboard-appears-in-ios?noredirect=1&lq=1)

## String

### Character nth element

```swift
extension StringProtocol {
    subscript(offset: Int) -> Character {
        self[index(startIndex, offsetBy: offset)]
    }
}
```

### isNumber

```swift
extension String {
    var isNumber: Bool {
        !isEmpty && rangeOfCharacter(from: .decimalDigits.inverted) == nil
    }
}
```
### Format

## Value Conversion


## Colors

Visit this [extension link](/ios/ui/uiColor#Extension)


## UIView

### Gradient Layer 

Adding a gradient layer to the background UIView object.
```swift
import UIKit
extension UIView {
	func addGradient(color1: CGColor,
				 color2: CGColor) {
		let gradientLayer = CAGradientLayer()
		gradientLayer.frame = bounds
		gradientLayer.colors = [color1, color2]
		layer.addSublayer(gradientLayer)
	}
}
```
https://www.advancedswift.com/gradient-view-background-in-swift/#override-layerclass-to-add-a-cagradientlayer

Class approach which is better due to dynamic layout orientation updates

```swift
class GradientView: UIView {
    let gradientLayer: CAGradientLayer = .init()
    init(_ colors: UIColor...) {
        super.init(frame: .zero)
        gradientLayer.frame = bounds
        gradientLayer.colors = colors.map(\.cgColor)
        layer.addSublayer(gradientLayer)
    }
    override func layoutSubviews() {
        super.layoutSubviews()
        gradientLayer.frame = bounds
    }
}
```

The func `layoutSubviews()` in my opinion would appropriately deal with framing when the UI is in the process of laying out subviews. Which would be when the user is changing orientation on its physical devices.


## Collection

Handy extensions for checking things when they are being conformed to protocol hashable elements.
```swift
extension Collection where Element: Hashable {
    func excludes(_ element: Element) -> Bool {
        return !self.contains(element)
    }
    
    var isNotEmpty: Bool {
        return !self.isEmpty
    }
}
```


## Dictionary

```swift
extension Dictionary {
    mutating func merge(dict: [Key: Value]){
        for (k, v) in dict {
            updateValue(v, forKey: k)
        }
    }

    func merged(dict: [Key: Value]) -> [Key: Value] {
        var newDict: [Key: Value] = self
        for (k, v) in dict {
            newDict.updateValue(v, forKey: k)
        }
        return newDict
    }
}
```

## Optional

Checking `isNil` condition for better readability.

```swift
extension Optional {
    var isNil: Bool {
        return self == nil
    }
}
```

## Limiting conformance

I need to understand the difference between `: Type` & `== Type`
Would have to check some articles around protocol conformance or extension conformance. I know that one is a protocol type and one is element reference check or something which is more expensive on CPU.

`: Type` 
```swift
extension Assert where TestValueType: Collection {
    public func isEmpty(message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {

        XCTAssertTrue(testValue.isEmpty, message(), file: file, line: line)

    }
}
```

`== Type`
```swift
extension Assert where TestValueType == Array<Any> {
    public func isEmpty(message: @autoclosure () -> String = "", file: StaticString = #filePath, line: UInt = #line) {

        XCTAssertTrue(testValue.isEmpty, message(), file: file, line: line)

    }
}
```


## Override

[swift | how-to-override-extension-methods](https://blog.flaviocaetano.com/post/this-is-how-to-override-extension-methods/)

## Resources

[swift by sundell | the-power-of-extensions-in-swift](https://www.swiftbysundell.com/articles/the-power-of-extensions-in-swift/)

