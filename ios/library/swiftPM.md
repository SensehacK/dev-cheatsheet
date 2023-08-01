
# Swift Package Manager

## Intro

Versatile yet out of beta package manager. Great support in built in Xcode IDE. 
Still initial adoption pain back in 2020, 2021. I think so past two years it has matured quite a bit.


## Errors

```
Not able to download packages properly.
```
Option in Menu bar.
Xcode ->  File -> Packages -> 
`Reset package cache`
& even not working then select `resolve packages`


```
Binary target 'LibraryName' could not be mapped to an artifact with the expected name 'LibraryName'
```

Deleting `~/Library/org.swift.swiftpm` helped for us
```sh
rm -rf ~/Library/org.swift.swiftpm
```

https://developer.apple.com/forums/thread/711597
