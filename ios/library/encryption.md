
## Data Protection

[apple docs | encrypting your app files](https://developer.apple.com/documentation/uikit/encrypting-your-app-s-files)

## Code

```swift
do {
   try data.write(to: fileURL, options: .completeFileProtection)
}
catch {
   // Handle errors.
}
```


[NS Data Writing options](https://developer.apple.com/documentation/foundation/nsdata/writingoptions)

