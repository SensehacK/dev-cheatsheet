


## Empty namespace
 
Better organization around the code in big projects. No need to initialize or privatize the init() function internally.


https://www.swiftbysundell.com/articles/powerful-ways-to-use-swift-enums/

https://stackoverflow.com/questions/49427144/is-there-a-technical-reason-to-use-swifts-caseless-enum-instead-of-real-cases


https://docs.swift.org/swift-book/LanguageGuide/Enumerations.html

https://www.swiftbysundell.com/basics/enums/




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