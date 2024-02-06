# UIColor


## Extension

You could define your colors extension in a separate folder and class file. That would better define your codebase in a cleaner approach. So it could be used anywhere in the project where it takes UIColor or Color class object of any sort.

```swift
// Extension Define
import UIKit
extension UIColor {
    static let kautilyaPrimaryColor = #colorLiteral(red: 0.6220935889, green: 0.9803921569, blue: 0.3810976606, alpha: 1)
}

// Utilize
 view.backgroundColor = .kautilyaPrimaryColor
```

You would get clean code and also direct shorthand autocompletion. Rather than writing verbose code like this

```swift
// Define
struct HSColors {
    // Colors
    static let sensehackDarkGrey = UIColor(red: 69/255, green: 69/255, blue: 69/255, alpha: 1)
}

// Utilize
view.backgroundColor = HSColors.sensehackDarkGrey;
// OR
view.backgroundColor = UIColor(red: 0.6220935889, green: 0.9803921569, blue: 0.3810976606, alpha: 1);
```


## Color Literal 

```swift
static let kautilyaPrimaryColor = #colorLiteral(red: 0.6220935889, green: 0.9803921569, blue: 0.3810976606, alpha: 1)
}
```

You can use `#colorLiteral(r:g:b:a:);` to hide the values of the color itself. Xcode just interprets and abstracts these values with a colored square. Double tap to edit it using the color dialog view or you can see its actual values in git.



## SwiftUI Migration

#### UIColor -> Color

Use Color for SwiftUI unless you want to explicitly convert UIColor to Color in its initializer or extension.

```swift
UIColor.primary
// Newer
Color.primary
```

#### foregroundColor -> foregroundStyle

Deprecated property code
```swift
// Old
.foregroundColor(.primary)
// New
.foregroundStyle(.primary)
```

## inverse color extension


[Code snippet from SO](https://stackoverflow.com/questions/5893261/how-to-get-inverse-color-from-uicolor/5901586#5901586)

```swift
func inverseColor() -> UIColor {
    var alpha: CGFloat = 1.0
    
    var red: CGFloat = 0.0, green: CGFloat = 0.0, blue: CGFloat = 0.0
    if self.getRed(&red, green: &green, blue: &blue, alpha: &alpha) {
        return UIColor(red: 1.0 - red, green: 1.0 - green, blue: 1.0 - blue, alpha: alpha)
    }
    
    var hue: CGFloat = 0.0, saturation: CGFloat = 0.0, brightness: CGFloat = 0.0
    if self.getHue(&hue, saturation: &saturation, brightness: &brightness, alpha: &alpha) {
        return UIColor(hue: 1.0 - hue, saturation: 1.0 - saturation, brightness: 1.0 - brightness, alpha: alpha)
    }
    
    var white: CGFloat = 0.0
    if self.getWhite(&white, alpha: &alpha) {
        return UIColor(white: 1.0 - white, alpha: alpha)
    }
    
    return self
}
```
## References

Resolved Color -> with system trait of appearance set.
[Apple dev | ui color resolver](https://developer.apple.com/documentation/uikit/uicolor/3238042-resolvedcolor) 