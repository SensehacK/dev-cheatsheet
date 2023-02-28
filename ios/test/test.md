# Test


## Test Pattern

## Unit Test

Every unit test follows this general pattern:  

1.  setup some object under test
2.  provide the object under test some input
3.  make assertions on the objects outputs




## Skip Tests

You can append `skip` to the test_function_name in order for Xcode compiler | runtime service to skip those tests in order to be ranned and not wasted with that resources accordingly.

Really handy when you're working with `flaky` tests


## Conditional Skip Testing

You could utilize the various ways to skip testing if certain conditions have been met.

```swift
guard let envValue = ProcessInfo.processInfo.environment["IS_CI_SERVER"] else { return }
try XCTSkipIf(envValue == "true")
```

You could embed this code in Test life cycle methods which is present for setting up code / environment before running the main test case.

- func setUp() { }
- func setUpWithError() throws { }

The `setUpWithError` is the right candidate for skipping tests without adding that skip_logic for every unit tests. You can just include that information in the Test_Class file.
Clean and less verbose.


## Links

https://stackoverflow.com/questions/64025146/skip-multi-tests-in-xcode

https://www.wwdcnotes.com/notes/wwdc20/10164/

https://developer.apple.com/documentation/xctest/3521325-xctskipif

https://developer.apple.com/documentation/xctest/xctest/3521150-setupwitherror

https://docs.fastlane.tools/actions/run_tests/

https://www.matrixprojects.net/p/skipping-tests-in-xcode/

https://medium.com/xcblog/speed-up-ios-ci-using-test-without-building-xctestrun-and-fastlane-a982b0060676