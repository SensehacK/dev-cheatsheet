
## Private API

Obviously an actual attribute or other feature would be superior, but in the meantime the best I can think of would be to make the implementation method internal and un-deprecated (and differentiated by e.g. an underscore), while having an equivalent (not underscored) forwarding public symbol marked deprecated, but make sure any internal call sites use the internal variant and not the public API.

## Rename deprecations

```swift
@available(*, deprecated, renamed: "newMethod")
func oldMethod() {}
func newMethod() {}
```


## Soft Deprecate

Apple (and the Swift project) uses `available: 9999` and `deprecated: 10000` to indicate availablility for future (unannounced) versions of OSes or Swift.


`deprecated: 10000` means "soft-deprecated", i.e. it's not deprecated now and will continue to function, but it's not recommended. It's the same value used in the `API_TO_BE_DEPRECATED` macro in `availability.h`.

[apple swift forums | deprecated](https://forums.swift.org/t/dont-see-any-deprecation-warning-due-to-deprecated-100000-0-whats-the-rationale-for-marking-it-this-way/38404/2)

## Warnings

Sometimes xcode doesn't show deprecate library or API warnings for specific OS version. Even if the target device which you're building for is the one which is deprecated for that OS. 
eg. iPhone 15 Pro Max - iOS 18.2 with Xcode 15 doesn't show API deprecated warnings which is deprecated for iOS 18.0++

Solution is to upgrade your IDE to support latest API / SDK base OS source. My problem was resolved when I opened the same project in Xcode 16 beta and it showed the warning in `documentation` popup.

> If your Deployment target is older than the version of iOS that the API was deprected in (so if your deployment targer is iOS 8.0 or lower), the compiler won't give you deprecation warnings for that API.
## References

[sarunw | deprecate-old-api-in-swift](https://sarunw.com/posts/deprecate-old-api-in-swift/)

[HWS | available deprecate](https://www.hackingwithswift.com/example-code/language/how-to-use-available-to-deprecate-old-apis)
