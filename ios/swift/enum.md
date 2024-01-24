# Enum


## Empty namespace
 
Better organization around the code in big projects. No need to initialize or privatize the init() function internally.

[swiftbysundell | enums](https://www.swiftbysundell.com/basics/enums/)

[swift by sundell | powerful-ways-to-use-swift-enums](https://www.swiftbysundell.com/articles/powerful-ways-to-use-swift-enums/)

[SO | caseless enums](https://stackoverflow.com/questions/49427144/is-there-a-technical-reason-to-use-swifts-caseless-enum-instead-of-real-cases)

[swift docs | enumerations](https://docs.swift.org/swift-book/LanguageGuide/Enumerations.html)


## Indirect Enums

Mostly used in Apple foundation or library frameworks in order to make references internally using enums.

```swift
indirect Node {
	case node(value: Node)
	case value(String)
}
```


## [Objective C Equivalent](ios/objectiveC/enum.md)


## Unit test


```swift
enum Security: String {
	case faceID, touchID, password, none
	var systemImageName: String { 
		return self.lowercased()
	}
}


final class SecurityTypeTests: XCTestCase {

	let testObject = Security.self

	func test_SystemImageName() throws {
	
		Assert(testObject.faceID.systemImageName).isEqual(to: "faceid")
		Assert(testObject.touchID.systemImageName).isEqual(to: "touchid")
		Assert(testObject.password.systemImageName).isEqual(to: "password")
		Assert(testObject.none.systemImageName).isEqual(to: "none")
		
		try test("returns non-nil when used with `UIImage.init(systemName:)`") {
			try testObject.allCases.forEach {
			_ = try Unwrap(UIImage(systemName: $0.systemImageName)) }
		}
	}

}
```



