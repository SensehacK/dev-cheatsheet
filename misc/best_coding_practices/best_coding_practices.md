# Best Coding Practices

## Intro

This is still a document maintained for my personal usage, I’m not advocating anyone that, below mentioned approach or design pattern is the best for solving a coding problem.

It varies from language to language and different background of problems. It doesn’t hurt to learn few different ways of solving the same problem and thus evaluating the efficiency while computing the time and space complexity of a problem solution.

> “Good design is half the battle” - Kautilya Save

Still linking a Wiki just for better read. [Wiki Coding Practices](https://en.wikipedia.org/wiki/Best_coding_practices)

## Safely Unwrapping

It is always good practice to check for ‘undefined’ / ‘null’ or you could optional chain the variable using ‘if let’ or ‘?’Syntax depending on your target language.

```text
 if let optional = class_Name.other_Class_ObjName?.property_Val {
  print("Safely unwrapped \(optional).")
 }
 else
 {
  print("Unable to retrieve the optional.")
 }
```



https://www.avanderlee.com/optimization/refactoring-swift-best-practices/

### Authored by : [Kautilya Save](https://sensehack.github.io/)

### [GitHub](https://github.com/SensehacK)

