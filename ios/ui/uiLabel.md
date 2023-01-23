uilabel


## Text alignment

[Alignment](https://iostechsolutions.blogspot.com/2014/04/uilabel-top-aligned-align-text-to-top.html)


## Margin Padding

[Margin](https://stackoverflow.com/questions/3476646/uilabel-text-margin#5155382)

[Padding](https://stackoverflow.com/questions/27459746/adding-space-padding-to-a-uilabel)


## Extension

[article](https://spin.atomicobject.com/2017/08/04/swift-extending-uilabel/)


## Multi line

This is the normal way of adding multiple lines. Important thing to remember you need to define your height/width constraints properly in order to have multiple line on a UILabel.

```swift
textLabel.lineBreakMode = .byWordWrapping
textLabel.numberOfLines = 0
```


Now if you have `NSAttributedString` define which gets added to the label

```swift
var attributedTitle: NSAttributedString = {
let title = NSMutableAttributedString(
   icon: Icon.flows,
   iconSize: Constants.iconSize,
   iconColor: labelTextColor)

let paragraphStyle = NSMutableParagraphStyle()
let textRange = NSRange(location: 0,
						length:title.length)
paragraphStyle.alignment = .center
paragraphStyle.minimumLineHeight = 12
title.addAttribute(.paragraphStyle,
				   value: paragraphStyle,
				   range: textRange)


// Setting the attributed text
textLabel.attributedText = attributedTitle
```

Remember that your minimumLineHeight could also come in picture with multi - line texts. It didn't help me overall but just letting this in the doc.


https://stackoverflow.com/questions/990221/multiple-lines-of-text-in-uilabel

https://www.hackingwithswift.com/read/24/4/formatting-strings-with-nsattributedstring

Caveats with baseline offset being added which could be non-zero, this would prematurely make the label truncated and the number of lines = 0 not being respected for having multi line support.

```swift
title.addAttribute(.baselineOffset,
				   value: 24,
				   range: NSRange
				   (location: 0,
				   length: element.length)
				   )
```