# TextField

### Programmatic

[Stack Overflow](https://stackoverflow.com/questions/24710041/adding-uitextfield-on-uiview-programmatically-swift)

### Text Attributes

The general form for making and setting an attributed string is like this. You can find other common options below.

```swift
// create attributed string 
let myString = "Swift Attributed String" let myAttribute = [ NSAttributedString.Key.foregroundColor: UIColor.blue ] 
let myAttrString = NSAttributedString(string: myString, attributes: myAttribute)
// set attributed text on a UILabel 
myLabel.attributedText = myAttrString
```

[Source](https://stackoverflow.com/questions/24666515/how-do-i-make-an-attributed-string-using-swift)

