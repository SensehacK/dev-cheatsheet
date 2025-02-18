# Access Control

## Options

- File private
- private
- public
- internal

## Error

### Inaccessible

```sh
initializer is inaccessible due to 'internal' protection level
```

Just define your struct or class with public initializer to have it explicitly setup for import or initialization.



## Local scope

```swift
private(set) var currentText: String = ""
```
This kinda mimics a `getter` property on the same variable rather than exposing more `Public` variables to the internet `setter` variables.  
Good design is always to mark everything local scope, final class, private variables/functions. Exposing less things to outside world is crucial in order to have a maintainable code-base as well as helps avoid mind mapping while debugging.


## [ObjC Equivalent of access_control](/ios/objectiveC/access_control.md)