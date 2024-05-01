# Best Coding Practices

## Intro

This is still a document maintained for my personal usage, I’m not advocating anyone that, below mentioned approach or design pattern is the best for solving a coding problem.

It varies from language to language and different background of problems. It doesn’t hurt to learn few different ways of solving the same problem and thus evaluating the efficiency while computing the time and space complexity of a problem solution.

> “Good design is half the battle” - Kautilya Save

Still linking a Wiki just for better read. [Wiki Coding Practices](https://en.wikipedia.org/wiki/Best_coding_practices)

## Safely Unwrapping

It is always good practice to check for ‘undefined’ / ‘null’ or you could optional chain the variable using ‘if let’ or ‘?’Syntax depending on your target language.

```swift
if let optional = class_Name.other_Class_ObjName?.property_Val {  print("Safely unwrapped \(optional).")
}
else {
 print("Unable to retrieve the optional.")
}
```

### Guard usage for unnecessary optional syntax

More example for avoiding unnecessary `?` `!` or `??` 

```swift
public override func isEqual(_ object: Any?) -> Bool {
 strID == (object as? VSS)?.strID
 && strSignal == (object as? VSS)?.strSignal
}
```

New Code

```swift
public override func isEqual(_ object: Any?) -> Bool {
 guard let vssO = object as? VSS else { return false }
 
 return strID == vssO.strID
 && strSignal == vssO.strSignal
}
```

## Formatting

[code_formatting](code_formatting.md)
[Code Linter](greenfield_code.md##Code%20Linter)

## Swift Specific Tips

[best_practices](best_practices.md)

## Pyramid of Doom

Avoiding pyramid of doom with if else identation.

[pyramid of doom](<https://en.wikipedia.org/wiki/Pyramid_of_doom_(programming)>)


## if else if 

[dangling else ambiguity](https://www.geeksforgeeks.org/dangling-else-ambiguity/)

## [Clean Code](architecture/terminologies/process_terms#Clean%20Code)







## Resources

[refactoring-swift-best-practices](https://www.avanderlee.com/optimization/refactoring-swift-best-practices)



### Authored by : [Kautilya Save](https://sensehack.github.io/)

### [GitHub](https://github.com/SensehacK)
