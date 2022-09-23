

## RxDataSource

Add `RxDataSources` from Package manager to the project.

```swift

struct TargetSection {
    var header: String
    var items: [Target]
}

extension TargetSection: SectionModelType {
    typealias Item = Target
    init(original: TargetSection, items: [Item]) {
        self = original
        self.items = items
    }
}

```



### Resources 

https://benoitpasquier.com/advanced-concepts-uitableview-rxdatasource/


https://stackoverflow.com/questions/46521042/rxswift-double-mapping-in-tableview-rx-itemselected


https://stackoverflow.com/questions/46811630/get-model-from-uicollectionview-indexpath/60926473#60926473