# Switch



## Implementation

```swift
enum Animal {
	case dog
	case cat
	case wolf
}

let animal: Animal = .wolf
switch animal {
	case ...
	default: 
}
```

## No - op

```swift
switch caseVar {
	case .caseOne: print("1")
	case .caseTwo: ()
	case .caseThree: break
}
```

SwiftUI ViewBuilder 
break does not work with ViewBuilder

```swift
switch caseVar {
	case .caseOne: print("1")
	case .caseTwo: EmptyView()
}
```

[SO | noop-for-swifts-exhaustive-switch-statements](https://stackoverflow.com/questions/24141900/noop-for-swifts-exhaustive-switch-statements)

### Break and Continue

[andybargh | break-and-continue](https://andybargh.com/break-and-continue/)


## if case let

The Swift If-Case-Let syntax is a convenient shortcut to avoid a full switch statement when you only want to match a single case.

[Pattern Matching](https://alisoftware.github.io/swift/pattern-matching/2016/03/27/pattern-matching-1/)
You can do switch statement on enums as well as do specific case if needed.

```swift
// event: Enum type
if case .caseOne(let msg) = event {
	self?.log(error.description, level: .error)
	self?.playerError = error
}
```

Nesting cases with if let Result & enum switch type
```swift
// urlResult: Result type & urlType: enum
if case let .success(urlType) = urlResult,
	case let .parsed(urlParsed) = urlType {
}
```
[use your loaf | swift-if-case-let](https://useyourloaf.com/blog/swift-if-case-let/)

if case let is an abbreviated form of switch
[gosh darn | If Case let](https://goshdarnifcaseletsyntax.com/)
[fucking if case let syntax](https://fuckingifcaseletsyntax.com/)


## Reference

[swift org | control flow](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/)
