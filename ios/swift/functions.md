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


## Variadic Parameters

You can skip using `array` type in the API definition and use variadic parameters introduced in Swift 5.0

```swift
extension Canvas {
    func add(_ shapes: Shape...) {
        shapes.forEach(add)
    }
}

let circle = Circle(center: CGPoint(x: 5, y: 5), radius: 5)
let lineA = Line(start: .zero, end: CGPoint(x: 10, y: 10))
let lineB = Line(start: CGPoint(x: 0, y: 10), end: CGPoint(x: 10, y: 0))

let canvas = Canvas()
canvas.add(circle, lineA, lineB)
canvas.render()
```

[Code snippet by Swift by Sundell](https://www.swiftbysundell.com/tips/using-variadic-parameters/)