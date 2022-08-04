Binder


To avoid having an extra subject for having inputs to the property.

```
public extension Session.Storage {
    var currentEntry: Session.Entry? { sessionEntryStack.last }
    func add(_ entry: Session.Entry) {
        sessionEntryStack.append(entry)
    }
```

```
extension Session.Storage: ReactiveCompatible { }

public extension Reactive where Base: Session.Storage {
    var addEntry: Binder<Session.Entry> {
        return Binder(base) { base, entry  in
            base.add(entry)
        }
    }
```



Extension Binder

UI Button
```
public extension Reactive where Base: UIView {
    var isVisible: Binder<Bool> {
        return Binder(self.base) { view, visible in
            view.isVisible = visible
        }
    }
}
```