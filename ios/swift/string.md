# String

## Manipulation


## Substring

```swift
let quote = "The revolution will be Swift"
let substring = quote.dropFirst(23)
let realString = String(substring)
```

Type conversion to String [HWS](https://www.hackingwithswift.com/example-code/language/how-to-convert-a-substring-to-a-string)


## Contains

```swift
let c = "C"
let objc = "Objective-C"
objc.contains(c)// true

objc.range(of: c, options: .caseInsensitive) != nil
objc.localizedCaseInsensitiveContains(c)

```

## Range




[sarunw |  different-ways-to-check-if-string-contains-another-string](https://sarunw.com/posts/different-ways-to-check-if-string-contains-another-string-in-swift/)



## Print

Printing boolean values in print statement wasn’t straight forward as I believed it was.
So we can encapsulate the boolean value in string and print it.

[SO](https://stackoverflow.com/questions/28136555/display-the-value-of-bool-in-swift)


## nth element

Very useful thread for getting character of string in swift, playing with its index values rather than just value of the string character.

```swift
let input = "Kautilya Save"
let char = input[input.index(input.startIndex, offsetBy: 0)]
print(char) // K

// Extension method
print(input[0] input[9]) // KS
```
[get-character-from-string-using-its-index-in-swift](https://www.simpleswiftguide.com/get-character-from-string-using-its-index-in-swift/)

You can also use an extension for it. [extensions Character nth element](/ios/lifecycle/extensions.md)

[SO](https://stackoverflow.com/questions/24092884/get-nth-character-of-a-string-in-swift-programming-language)

[Simple Swift guide](https://www.simpleswiftguide.com/get-character-from-string-using-its-index-in-swift/)


## Range

```swift
let c = "C"
let objc = "Objective-C"

objc.range(of: capitalC) != nil// true
```


[SO](https://stackoverflow.com/questions/28182441/swift-how-to-get-substring-from-start-to-last-index-of-character)


## Computed string _ closure 

Pass parametric property like behavior but Swift doesn't allow for parameters to be passed to properties. So we would use function - closure(nameless function) to achieve the same goal.

```swift
var image_: (String) -> String {
	{ "image-\($0)" }
}
// Call
print(image_("3"))
```


## Expressible Literals

Good article about what they are and how they are used.
[avanderlee | expressible-literals](https://www.avanderlee.com/swift/expressible-literals/)

## Performance

String concatenation `+` is faster than `\(string_variable)` in the code according to this below document.

```swift
let name = "Kautilya"
let str1: String = "Hi! my name is \(name)"
let str2: String = "Hi! my name is " + name
```


[concatenating-strings-in-swift-which-way-is-faster](https://www.globalnerdy.com/2016/02/03/concatenating-strings-in-swift-which-way-is-faster/)


## Multi Line String

```swift
var str1 = """
This goes
over multiple \
lines
"""
```

[HWS | Code snippet](https://www.hackingwithswift.com/sixty/1/3/multi-line-strings) 

## CFString

```swift
// %@    Objective-C object, printed as the string returned by descriptionWithLocale: if available, or description otherwise.
String(format: "%@", ["Hello", "world"])
```


```swift
// %%    '%' character.
String(format: "100%% %@", true.description)
```

```swift
// %d, %i    Signed 32-bit integer (int).
String(format: "from %d to %d", Int32.min, Int32.max)
```


```swift
//  %u, %U, %D    Unsigned 32-bit integer (unsigned int).
String(format: "from %u to %u", UInt32.min, UInt32.max)
```

> 

```swift
// %x    Unsigned 32-bit integer (unsigned int), printed in hexadecimal using the digits 0–9 and lowercase a–f.
String(format: "from %x to %x", UInt32.min, UInt32.max)
```


```swift
// %X    Unsigned 32-bit integer (unsigned int), printed in hexadecimal using the digits 0–9 and uppercase A–F.

String(format: "from %X to %X", UInt32.min, UInt32.max)
```


```swift
// %o, %O    Unsigned 32-bit integer (unsigned int), printed in octal.
String(format: "from %o to %o", UInt32.min, UInt32.max)
```


```swift
// %f    64-bit floating-point number (double), printed in decimal notation. Produces "inf", "infinity", or "nan".

String(format: "from %f to %f", Double.leastNonzeroMagnitude, Double.greatestFiniteMagnitude)
```




[Apple archive | Format specifiers](https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFStrings/formatSpecifiers.html)

Copied from [SO | Swift string format specifiers](https://stackoverflow.com/questions/52332747/what-are-the-supported-swift-string-format-specifiers)


## Deprecations

[String interpolation Debug description](https://izziswift.com/how-to-solve-string-interpolation-produces-a-debug-description-for-an-optional-value-did-you-mean-to-make-this-explicit-in-xcode-8-3-beta/)
