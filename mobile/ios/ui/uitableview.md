UI TableView


## Initialization


## Delegates


## Customizability


## Extension

Unselecting the selected tableview

[SO](https://stackoverflow.com/questions/3968037/how-to-deselect-a-selected-uitableview-cell)

```swift
import UIKit

extension UITableView {

    func deselectSelectedRow(animated: Bool)
    {
        if let indexPathForSelectedRow = self.indexPathForSelectedRow {
            self.deselectRow(at: indexPathForSelectedRow, animated: animated)
        }
    }

}
```


## Reusability


Properly reset the attributes of the table view cell so that it doesn’t take a performance hit even when using “prepareToReuse” method call.

[Apple docs prepareToReuse](https://developer.apple.com/documentation/uikit/uitableviewcell/1623223-prepareforreuse)

[duplicate cells](https://fluffy.es/solve-duplicated-cells/)


## Errors

### Constraints Error

Warning: Detected a case where constraints ambiguously suggest a height of zero
[SO](https://stackoverflow.com/questions/25902288/detected-a-case-where-constraints-ambiguously-suggest-a-height-of-zero)