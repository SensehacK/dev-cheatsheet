
# Command Line Arguments

## Syntax

This lets us easily access any command line argument passed into our program as "-path":

```swift
guard let path = UserDefaults.standard.string(forKey: "path") else {
    throw Error.noPathGiven
}

let url = URL(fileURLWithPath: path)

do {
    let data = try Data(contentsOf: url)
    ...
} catch {
    throw Error.failedToLoadData
}
```

[Code snippet from source | swift by Sundell](https://www.swiftbysundell.com/articles/working-with-files-and-folders-in-swift/)

## Reference

[Launch arguments in Swift](https://www.swiftbysundell.com/articles/launch-arguments-in-swift)