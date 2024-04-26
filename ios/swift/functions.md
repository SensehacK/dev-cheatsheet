# functions



## Mutable variables as parameters

```swift



```
[Hacking With Swift](https://www.hackingwithswift.com/sixty/5/10/inout-parameters)

[nshipster | method-swizzling](https://nshipster.com/method-swizzling/)


## Result return value Discard

Discardable result

You are getting this issue because the function you are calling returns a value but you are ignoring the result.

There are two ways to solve this issue:

1. Ignore the result by adding `_ =` in front of the function call
    
2. Add `@discardableResult` to the declaration of the function to silence the compiler

```swift
@discardableResult
func doSomething() -> String { return "Custom String"}

doSomething()

let _ = doSomething()

```

## Selector Obj C

**_Unrecognized Selector Sent To Instance_**

[unrecognized-selector](https://becodable.com/unrecognized-selector-sent-to-instance/)
