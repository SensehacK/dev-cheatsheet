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



## Adding links to Doc

You can define markdown links or reference them as a link node in the documentation information.
```swift
/**
  Defines the OSLog's logging levels to categorize priority and messaging.

  [OS Log - Logger Library Reference]: https://developer.apple.com/documentation/os/logger "Logger"

  ### **Useful Links**

  * [OS Log - Logger Library Reference]

 */
 enum LogType: String { }
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


Publishing to Github Actions Pages via Swift DocC
https://www.kodeco.com/40047657-docc-tutorial-for-swift-automating-publishing-with-github-actions

Hosting it locally using local server follow [this guide](tools/server/http-server#Quick%20run)

## DocC Errors

### swift docc empty webpage

Error 404 for js and css files
```error
GET[https://sensehack.github.io/css/index.038e887c.css]
GET[https://sensehack.github.io/js/chunk-vendors.ba2dd0cb.js]
```

If the swift docc is blank on our CI/CD server probably you forgot to update the `--hosting-base-path` of it in order for Github Actions / Pages to properly get its references.


### jobs failed

Sometimes your xcodebuild fails and the job swift docc command line would state errors which aren't in correlation with it. So make sure you build locally first with codebase and then push new changes in order to avoid anxiety on what's wrong with your CI/CD. 

```error
Error: '/Users/runner/work/swift-docc/swift-docc/.derivedData/Build/Products/Debug-iphonesimulator/swifty-docc.doccarchive' is not a valid DocC Archive. Expected a directory but a path to a file was provided

Usage: docc process-archive transform-for-static-hosting <source-archive-path> [--output-path <output-path>] [--hosting-base-path <hosting-base-path>]

See 'docc process-archive transform-for-static-hosting --help' for more information.

./build_docc.sh: line 40: docs/index.html: No such file or directory

Error: Process completed with exit code 1.
```

This time I forgot to add `func` in my `.swift` file for defining new public function but because I was building it as swift package, I never bothered to compile it and my `shell` script never runs xcode build it runs `docbuild` command which I believe internally runs `build` command but the error would be a bit ambiguous and couldn't point you to the right direction at first. Makes you wonder version control and change management tools like git and semver are devil's tools to properly defeat the bugs or isolate them in a concise manners. This time we don't have to [goat for a ritual](https://en.wikipedia.org/wiki/Baphomet).



### Target Issues

This fails on xcode build docC command because our project structure has defined `.xcWorkspace` as a hodgepodge of Swift Package Manager, Libraries, frameworks, TestUI Target -> iOS App. Hence we need to specify the `workspace` in our build command or else it won't find the necessary products/ targets in the project file.

```log
/Users/user/git/cloud/reponame-apple/TestUI/TestUI.xcodeproj: error: Missing package product 'DependencyKit' (in target 'TestUI' from project 'TestUI')
```

You can actually use this bash snippet 

```sh
# scheme name
TARGET_SCHEME="TestUI"
# workspace name
WORKSPACE_NAME="TestUIP.xcworkspace"
DERIVED_DATA_PATH="docc"

# Actual build command
xcodebuild docbuild \
-workspace $WORKSPACE_NAME \
-scheme $TARGET_SCHEME \
-derivedDataPath $DERIVED_DATA_PATH \
-destination 'generic/platform=iOS';
```



### Architecture build issues

You can get away with this error since one of your dependency still doesn't support newer architectures like `arm64` for M1, Mx (ARM) architecture translation.

```sh
note: '/Users/user/git/cloud/reponame-apple/docc/SourcePackages/artifacts/client-spm-manifest/client/client.xcframework' is missing architecture(s) required by this target (arm64), but may still be link-compatible. (in target 'TestUI' from project 'TestUI')
```

 So you can change the `-destination` from `iOS Simulator` to `iOS` to just build for an architecture supported by your deprecated / old / not updated library / framework.
```sh
DESTINATION_PLATFORM_VALUE="generic/platform=iOS\ Simulator"
# Newer
DESTINATION_PLATFORM_VALUE_NEW="generic/platform=iOS"

# Actual build command
xcodebuild docbuild \
-destination $DESTINATION_PLATFORM_VALUE_NEW;
```

## Markdown

Markdown support has been added for Swift documentation in order to make the text formatting easier to write and consume.
https://www.appcoda.com/swift-markdown/



## Reference

https://developer.apple.com/library/archive/documentation/Xcode/Reference/xcode_markup_formatting_ref

https://cocoacasts.com/organize-your-swift-project-with-annotations-todos-and-fixmes

https://sarunw.com/posts/swift-documentation/

https://nshipster.com/swift-documentation/