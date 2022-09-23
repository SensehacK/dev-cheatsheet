# Doubts




Why convert to observable for RxCocoa UI elements

```
// Button
let button = closeButtonItem
            .rx
            .tap
            .asObservable()
            .withUnretained(self)
            .subscribe(onNext: { owner, _ in
               owner.dismiss(animated: true)
           })
           .disposed(by: self.disposeBag)

// Deselect the selected row
        tableView
            .rx
            .itemSelected
            .withUnretained(self)
            .subscribe(onNext: { owner, indexPath in
                owner.tableView.deselectRow(at: indexPath, animated: true)
            })
            .disposed(by: disposeBag)
```
            