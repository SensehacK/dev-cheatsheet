# String

## Manipulation


## Substring

Type conversion to String [HWS](https://www.hackingwithswift.com/example-code/language/how-to-convert-a-substring-to-a-string)


## Print

Printing boolean values in print statement wasn’t straight forward as I believed it was.
So we can encapsulate the boolean value in string and print it.



[SO](https://stackoverflow.com/questions/28136555/display-the-value-of-bool-in-swift)


## nth element
Very useful thread for getting character of string in swift, playing with its index values rather than just value of the string character.

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

## Deprecations

[String interpolation Debug description](https://izziswift.com/how-to-solve-string-interpolation-produces-a-debug-description-for-an-optional-value-did-you-mean-to-make-this-explicit-in-xcode-8-3-beta/)