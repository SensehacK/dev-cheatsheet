# Switch



## Implementation





## One case


if case let is an abbreviated form of switch
[If Case let](https://goshdarnifcaseletsyntax.com/)
https://useyourloaf.com/blog/swift-if-case-let/

[Pattern Matching](https://alisoftware.github.io/swift/pattern-matching/2016/03/27/pattern-matching-1/)


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


https://stackoverflow.com/questions/24141900/noop-for-swifts-exhaustive-switch-statements

### Break and Continue
https://andybargh.com/break-and-continue/

## Reference

https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/