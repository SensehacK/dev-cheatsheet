# UITableViewCell


## Guide

[Custom Nib](https://izziswift.com/custom-uitableviewcell-from-nib-in-swift/)

[Raywenderlich](https://www.raywenderlich.com/books/uikit-apprentice/v9.0/chapters/33-custom-table-cells)

[SO](https://stackoverflow.com/questions/24170922/creating-custom-tableview-cells-in-swift)

[Custom Cell](https://slicode.com/how-to-create-custom-tableview-cell-in-swift/)
## Deprecation
`textLabel` iOS 3.0–14.0 Deprecated
```swift
cell.textLabel?.text = "Hello!"
```

https://developer.apple.com/documentation/uikit/uitableviewcell/1623210-textlabel
should be switched to 
```swift
var content = cell.defaultContentConfiguration()
content.text = "Hello Kautilya"
content.secondaryText = "SK"
cell.contentConfiguration = content
```
https://medium.com/geekculture/modern-configurations-for-cells-and-views-after-ios-14-0-33b5c82ac448



