
# Test Errors



##  XCUITest Failed to terminate app

[SO | xcuitest-class-teardown-isnt-deleting-the-app-but-works-if-its-instance-teardow](https://stackoverflow.com/questions/73759977/xcuitest-randomly-failing-during-teardown-failed-to-terminate-com-bundle-id?noredirect=1&lq=1)

### XCUITest doesn't delete app

```swift
override func tearDown() {
    XCUIApplication().terminate()
    super.tearDown()
}
```


[SO | XCUITest Class teardown isnt deleting the app. But works if its instance teardown. What am I doing wrong?](https://stackoverflow.com/questions/53181823/xcuitest-class-teardown-isnt-deleting-the-app-but-works-if-its-instance-teardow)
