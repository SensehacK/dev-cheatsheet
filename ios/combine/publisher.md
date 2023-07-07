

## Create

By utilizing property wrapper we can just decorate any variable with `@Pubished` to make it publish-eable

```swift
@Published var someVariable: String = ""
```

UserDefault custom propery wrapper example [codable](codable.md)

Note:
Well suited for SwiftUI + Combine.
`willSet` internally it calls so that SwiftUI can make optimizations towards what should be refreshed on the UI when compared directly to `CurrentValueSubject` [subjects](subjects.md)

## Create custom Publisher

https://developer.apple.com/documentation/combine/publisher



https://www.swiftbysundell.com/articles/building-custom-combine-publishers-in-swift/

https://thoughtbot.com/blog/lets-build-a-custom-publisher-in-combine


## Reference

Great article about how reactive paradigm works in a way. Touches how we can support pre iOS 13 deployment targets and make use of custom property wrappers to have a temporary migration solution for older devices. Or we can use community adopted RxSwift reactive framework to work with it. Either way this article sheds a light on approaching a problem with 3 different ways which I always prefer when making those architectural decisions.
https://www.swiftbysundell.com/articles/published-properties-in-swift/ 

[thoughts on number 3](ReadME_thoughts.md)


Connecting and merging Combine publishers in Swift
https://www.swiftbysundell.com/articles/connecting-and-merging-combine-publishers-in-swift/


Core location example 
https://brightdigit.com/tutorials/combine-corelocation-publishers-delegates/

https://shareup.app/blog/how-to-clean-up-resources-when-a-combine-publisher-is-cancelled/