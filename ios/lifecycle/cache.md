# Cache

## Intro

Caching is an important topic and doing it right is sometimes very hard.
Lots of topics to cover in Caching mechanism. Here we just go through basic stuff about Caching.

## Manager


```swift
class CacheManager {
	// Singleton
	static let shared = CacheManager()
	private init() { }

	func configure() { 
		URLCache.shared = CachedSession.sessionUrlCache
	}
	
	func clearCache() {
		URLCache.shared.removeAllCachedResponses()
	}
	

	func saveCache() {
		queue.sync(flags: .barrier, execute: {
            try? saveToDatabaseManager()
        })
	}
}
```


## Cache Config

```swift
class CachedSession {
	static var sessionUrlCache: URLCache = {
        return URLCache(memoryCapacity: 1024 * 1024 * 200 ,
                                   diskCapacity: Int.max,
                                   diskPath: nil)
    }()					
}

```

It equals approximately 209 MegaBytes of Cache storage.


## Image Cache




## Caching Dictionary

### Theory

Since Swift Dictionaries or in dictionaries in general conform to `Hashable` protocol which means every time we add a value the hasher function creates a unique ID to quickly reference that in the Dictionary. Which is why we can get Time complexity of O(1) which is the fastest I believe.  
And there is also less CPU performance hit because for the past decade or so CPU have inbuilt hardware accelerator chips to do these kind of hashing mechanism on the fly and dedicated chip modules make CPU context switching back & forth pretty inexpensive.

Source my [own MR about my helper swift package](https://github.com/SensehacK/swift-sense/pull/3) for swift related projects (iOS, macOS, tvOS, watchOS) apps



## References

[deep dive urlrequest cache policy](https://medium.nextlevelswift.com/urlrequest-cache-policy-f7c30a96b698)

[heroku | increasing performance with http cache headers](https://devcenter.heroku.com/articles/increasing-application-performance-with-http-cache-headers)

[How to leverage HTTP cache in iOS](https://fabernovel.github.io/2019-01-22/how-to-leverage-http-cache-in-ios)

[cache & combine in iOS](https://pyartez.github.io/networking/simple-offline-caching-in-swift-and-combine.html)
