# Struct


## Choose Struct over class

[SO Discussion](https://stackoverflow.com/questions/24232799/why-choose-struct-over-class/24232845)


## Dynamic Member lookups

```swift
@dynamicMemberLookup
struct Car {
    subscript(dynamicMember member: String) -> String {
        let properties = ["brand": "Dodge", "name": "Viper SRT"]
        return properties[member, default: ""]
    }
}


let favCar = Car()
print(favCar.brand)
print(favCar.name)
```
https://www.hackingwithswift.com/articles/55/how-to-use-dynamic-member-lookup-in-swift


## Private Initializer

Structs do provide default initializers but if we want to expose them we need to define them as public init.
https://docs.swift.org/swift-book/documentation/the-swift-programming-language/accesscontrol/#Default-Memberwise-Initializers-for-Structure-Types

