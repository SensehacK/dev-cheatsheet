# String

## Manipulation


## Substring

```swift
let quote = "The revolution will be Swift"
let substring = quote.dropFirst(23)
let realString = String(substring)
```

Type conversion to String [HWS](https://www.hackingwithswift.com/example-code/language/how-to-convert-a-substring-to-a-string)


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

You can also use an extension for it. [extensions Character nth element](ios/lifecycle/extensions.md)

[SO](https://stackoverflow.com/questions/24092884/get-nth-character-of-a-string-in-swift-programming-language)

[Simple Swift guide](https://www.simpleswiftguide.com/get-character-from-string-using-its-index-in-swift/)


## Range

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


## Deprecations

[String interpolation Debug description](https://izziswift.com/how-to-solve-string-interpolation-produces-a-debug-description-for-an-optional-value-did-you-mean-to-make-this-explicit-in-xcode-8-3-beta/)
