# Enum


## namespace

Empty namespace
Better organization around the code in big projects. No need to initialize or privatize the init() function internally.

[swiftbysundell | enums](https://www.swiftbysundell.com/basics/enums/)

[swift by sundell | powerful-ways-to-use-swift-enums](https://www.swiftbysundell.com/articles/powerful-ways-to-use-swift-enums/)

[SO | caseless enums](https://stackoverflow.com/questions/49427144/is-there-a-technical-reason-to-use-swifts-caseless-enum-instead-of-real-cases)

[swift docs | enumerations](https://docs.swift.org/swift-book/LanguageGuide/Enumerations.html)

[swift forums | enum based namespaces](https://forums.swift.org/t/an-enum-based-approach-to-namespaces/12487)

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


## [Random element](ios/swift/random#Enum)



## Test data refactor enum

Code in question

```swift
let audioTrack1: AudioTrackable = AudioTrack(id: "English (US)", language: Locale(identifier: "en-US"), type: .audio, codecs: ["soun"])
let audioTrack2: AudioTrackable = AudioTrack(id: "English (US)", language: Locale(identifier: "en-"), type: .audio, codecs: ["soun"])
let audioTrack3: AudioTrackable = AudioTrack(id: "Enagas  (US)", language: Locale(identifier: "en-eS"), type: .audio, codecs: ["soun"])
let audioTrack4: AudioTrackable = AudioTrack(id: "English  x1(US)", language: Locale(identifier: "en-US"), type: .audio, codecs: ["soun"])
```

> Would it help to store these language values in some sort of enum ?

My answer for Framework based team
Since this is a test data I would think it would be overkill but I have already seen this implemented twice. So I get the refactor thing.
But on the same end we are an API / Library / Framework team so don't know if this would add any incentive as 
1. Its not consumer facing string or UI stakeholders
2. No localization support needed
3. No client data is being wrapped with these things
