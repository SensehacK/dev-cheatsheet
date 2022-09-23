UI TableView


## Initialization


## Delegates


## Customizability


## DataSource



## Diffable DataSource

`UITableViewDiffableDataSource`

https://medium.com/@ali-akhtar/uitableview-diffable-datasource-part-1-13a24e8f23d8


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

### Footer Empty cell

[SO](https://stackoverflow.com/questions/19911536/how-to-add-footer-view-for-uitableview-in-ib-when-working-with-storyboards)

[Show UITableView footer when empty SO](https://stackoverflow.com/questions/36330344/show-uitableview-footer-when-empty)

## Updates

iOS 15 TableViewCell reconfigure
[UITableView: reconfigure](https://twitter.com/smileyborg/status/1403908057185144832?lang=en)

Programmatic UITableView
https://martinlasek.medium.com/tutorial-adding-a-uitableview-programmatically-433cb17ae07d