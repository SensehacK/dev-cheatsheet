
# Introduction

Writing descriptive test case names are most important when working with complex codebase.
When there is a test failure on some unit tests locally or a CI server, you can easily pin point why that error happened and which logical scenario was not met. It helps us to easily navigate through the debug logs when using a suffix, prefix and also the test result expectations.


## Example

One of those examples include.

```swift
func test_whenNetworkIsNotReachable_andLoginRequestPasswordDoesNotMatchOfflinePassword_thenValidateForSessionTimeoutResultIsFailureWithInvalidPasswordError() throws { } 
```

Which helps us to be verbose and be distinct in the same scenario which is helpful when we have lots of tests in the project.


## Reflection or Mirror

APIs which creates its own unit tests structure data in order to easily isolate changeset and work with it.

## Mock
