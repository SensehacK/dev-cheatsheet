# Documentation

You can defined your own documentation while coding for your functions to be properly documented with the parameter types, information of what it would return with different type of conditions. I believe that in most of the projects were we already can inspect the codebase of a function to better understand, it doesn’t matter but for quick glance to get the bird eye view of the calling method is great. Also it is more future proof in terms of less work ahead if you wanted to make the whole class in a package library type of scenario.

## Headers

// MARK:

// TODO:

// FIXME: 



### Old Headers

In objective C we have pragma mark, we can utilize **MARK:** 
```text
You can use // MARK:

There has also been discussion that liberal use of class extensions might be a better practice anyway. Since extensions can implement protocols, you can e.g. put all of your table view delegate methods in an extension and group your code at a more semantic level than #pragma mark is capable of.
```
[SO](https://stackoverflow.com/questions/24017316/pragma-mark-in-swift?rq=1)


## Auto Completion

If you really like auto completion for your own internal methods, this is the way to do it. Also you can `command + click` on your function initializer with parameters in order to directly generate documentation stubs for you. Or you can manually enter them with appropriate parameters and back slashes.

```swift
  /// This is the initializer to invoke the web request class.
  /// - Parameters:
  ///   - fullName: Provide full name in string format
  ///   - email: Provide email in string format
  ///   - password: Provide password in string format
  init(fullName: String, email: String, password: String) {
  self.fullName = fullName
  self.email = email
  self.password = password
}
```



## Reference

https://cocoacasts.com/organize-your-swift-project-with-annotations-todos-and-fixmes