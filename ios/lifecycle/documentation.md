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


## Adding Comments


### Normal comment

```swift
let my_array = [a,b,c,d,e]
# my_array[1] # b

# Execute something
doSomething()
func doSomething() {
	print("Hello")				
}
```

### Multi line comment
```swift
let my_array = [a,b,c,d,e]
/*
my_array[1] # b

doSomething()
func doSomething() {
	print("Hello")				
}
*/
print("After multi line comment")
```

### Benefits of Multi line comment
- Less git diff since it is only 2 lines of code change
- Easier to read / review when Code Review
- Quickly you can toggle big chunk of commented out code or lane. 

```swift
// /* 
Some nonsensical stuff here
// */
```

## Functions Doc example

```swift
/**
Makes a network request using Generic type T: Codable and returns the two completioner handlers - Parsing & Result Type.
Consuming this API is quite easy and it also gives us an option to parse the network data response in the completion handler
- Parameter parse: Call internal parsing closure
- Parameter completion: Return Result(success, failure) `T:Codable` value
- Returns: Result<T? ,Error>
- Warning: Safely unwraping of `T:Codable` is consumer's responsibility.
	```
	Webservice().fetch(url: url) { }
	```
*/
 public func fetch<T: Codable>(url: URL,
    completion: @escaping (Result<T?, NetworkError>) -> Void)  { }
```

This lets us specify code as well in the docs or when xcode `Build Documentation` in Product Menu bar. This nicely compiles markdown format into the `Documentation` window. Or you can use `Dash` on macOS for your quick references.


## Swift DocC


Spent approx 45 mins deciphering why my github pages wasn't showing the Swift DocC generated static site. Turns out the url for target path component is also lowercase as pointed out by this SO post.

Note that my repository name was lowercase so I used `-hosting-base-path foobar`. The target path component, however, is always lowercase, Idk why.
https://stackoverflow.com/a/71199418/5177704



Great tool to use for generating documentation for your project. As long as you document things properly.



https://developer.apple.com/documentation/docc
Xcode 13
https://www.wwdcnotes.com/notes/wwdc21/10166/

https://developer.apple.com/videos/play/wwdc2021/10236/

https://developer.apple.com/videos/play/wwdc2022/110369/

Kodeco 
https://www.kodeco.com/34919511-docc-tutorial-for-swift-getting-started
## Reference

https://cocoacasts.com/organize-your-swift-project-with-annotations-todos-and-fixmes

https://sarunw.com/posts/swift-documentation/

https://nshipster.com/swift-documentation/