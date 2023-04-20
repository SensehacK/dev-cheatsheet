

## Intro

Caching is an important topic and doing it right is sometimes very hard.


## Caching Dictionary

### Theory

Since Swift Dictionaries or in dictionaries in general conform to `Hashable` protocol which means every time we add a value the hasher function creates a unique ID to quickly reference that in the Dictionary. Which is why we can get Time complexity of O(1) which is the fastest I believe.  
And there is also less CPU performance hit because for the past decade or so CPU have inbuilt hardware accelerator chips to do these kind of hashing mechanism on the fly and dedicated chip modules make CPU context switching back & forth pretty inexpensive.

Source my [own MR about my helper swift package](https://github.com/SensehacK/swift-sense/pull/3) for swift related projects (iOS, macOS, tvOS, watchOS) apps
