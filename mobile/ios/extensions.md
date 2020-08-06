# Extensions

Swift plays a great role in terms of extending current functionality in a clean code aspect and not cluttering the main class code implementation.

So with extensions you could just extend specific functionality to a specific class by just defining `extension className`

## Colors

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

Note you can use `#colorLiteral(r:g:b:a:);` to hide the values of the color itself. Xcode just interprets and abstracts these values with a colored square. Double tap to edit it using the color dialog view or you can see its actual values in git.

## Alerts

## Keyboard

[Keyboard Dismiss](https://stackoverflow.com/questions/11282449/move-uiview-up-when-the-keyboard-appears-in-ios?noredirect=1&lq=1)



## String Format

## Value Conversion

