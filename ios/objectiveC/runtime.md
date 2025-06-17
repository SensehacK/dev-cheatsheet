


## init not available to subclass


Code snippet
```swift
class MockAssetResourceLoader: AVAssetResourceLoader {
    
    // built-in `init` is not available to subclasses so this takes advantage of obj C run time to create the mock
    static func makeResourceLoader() -> MockAssetResourceLoader {
        let allocated = MockAssetResourceLoader.perform(NSSelectorFromString("alloc"))
        return allocated?.takeRetainedValue() as! MockAssetResourceLoader
    }
}

class MockResourceLoadingRequest: AVAssetResourceLoadingRequest {
    static func makeLoadingRequest(_ url: URL, containsInfo: Bool) -> MockResourceLoadingRequest {
        let allocated = MockResourceLoadingRequest.perform(NSSelectorFromString("alloc"))
        let objcInstance = allocated?.takeRetainedValue() as! MockResourceLoadingRequest
        objcInstance.url = url
        objcInstance.hasContentInformationRequest = containsInfo
        return instance
    }
}
```
