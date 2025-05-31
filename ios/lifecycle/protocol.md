# Protocol

## Things to Remember

protocols can't have default implementation directly - just use extensions.
protocols can only have getters no setters.
Protocols can't have default parameters in a func. Of course remember that.
protocol variables can't be immutable

## Why protocols

> why did we need to add a protocol? Could we not have just added the functions to the class

My reasoning:
This is keeping up with good approach on test-ability of this feature for unit tests and support dependency injection in future. 
It also could be used as a TODO: marker when you have protocols with functions definition defined which needs to be implemented.

> what made you make this a protocol? b/c we could easily made this a function, just your thought process around it.

- Having protocol makes it easier for the implementer to not introduce more things than necessary. So you start with what is the MVP of that same class, function or properties.
- It also kinda helps in dependency injection and creating mocks in unit tests.
- It helps us to also easily allow us to pass protocol as a type for future generics using Protocols with associated types
- It helps the conforming object/instance of the protocol to have default implementation via `protocol extensions`. Thus guaranteeing default behavior like an optional default nil `let unwrappedValue = optionalValue ?? defaultValue`

## Combining Protocols

```swift
typealias DiskWritableByEncoding = DiskWritable & Encodable

struct TodoList: DiskWritableByEncoding {
    var name: String
}

var identityToken: NSObjectProtocol & NSCopying & NSCoding 
var array: [NSObjectProtocol & NSCopying & NSCoding]

func foo(param: NSObjectProtocol & NSCopying & NSCoding) { }
```

Code snippet from the article [swiftbysundell | combining-protocols-in-swift](https://www.swiftbysundell.com/articles/combining-protocols-in-swift/)

## Errors

### Accessible enclosing type 

This kind of error popped up for me even when my internal library had made this function public and my protocol was also public.
It seems Swift compiler was having issue with which public function it is referring towards.

```log
Method 'log(_:logType:)' must be as accessible as its enclosing type because it matches a requirement in protocol
```

Protocol Code

```swift
import Library_Code

public protocol Logable {
    var subCategory: SubCategory { get }
    var logLevel: LogType { get }
    func log(_ message: String, logType: LogType?)
}

public extension Logable {
    func log(_ message: String, logType: LogType? = .info) {
        VLogger.shared.log(subCategory, logType: level ?? logLevel, "\(message)")
    }
}
```

Library Implementation Code

```swift
public final class VLogger {
	public func log(_ category: SubCategory, logType: LogType = .info, _ message: String) { }
}
```

### variables cannot be immutable

```sh
Protocols cannot require properties to be immutable; declare read-only properties by using 'var' with a '{ get }' specifier
```

### cannot find type protocol in scope

Sometimes if the protocol has same name define in different scope and you're in different project scope with imported frameworks/libraries. You can get this error. 

```error
error: cannot find type 'Logable' in scope
```

Code

```swift
// In Parent scope
// Logable.swift

public protocol Logable { }
```

```swift
// In Child Library scope
// Logable.swift

public protocol Logable { }


// Can't find Logable in scope
class ImplementLog: Logable { } 
```

Even if you rename the protocol name it still is not able to distinguish itself. Might as well change the file name of the protocol. So that the newer protocol of similar name can be picked up by Xcode auto complete. It seems xcode or swift toolchain doesn't generate the new protocol interface bridging headers until there's some actual file name changes. For optimization reasons maybe or cache build control. I don't know but my money is on those two reasons why it doesn't pick those new changes.

Changes to make Xcode not give compile errors

```swift
// In Parent scope
// Logable2.swift
public protocol Logable2 { }
```

```swift
// In Child Library scope
// Logable.swift
public protocol Logable { }

// Now it can find Logable in scope
class ImplementLog: Logable { } 
```

## Protocol with Associated Types

Protocol with Associated types help write less code but adds more complexity towards maintaining and casting variables overall.

```swift
public protocol Trackable {
    associatedtype trackType: RawRepresentable where trackType.RawValue: StringProtocol
    var id: String { get }
    var language: Locale? { get }
    var type: trackType { get }
}

public struct TextTrack: Trackable {
    public let id: String
    public let language: Locale?
    public let type: TextType
    public let role: TextTrackRoles
}
public enum TextType: String {
	case normal, different 
}


public struct AudioTrack: Trackable {
    public let id: String
    public let language: Locale?
    public let type: AudioType
    public let codec: String
}
public enum AudioType: String {
	case normal, different 
}
```

But you kinda lose some type safety when you use associated types and now you're limiting yourself to only `Trackable` option.

Now you would have to force cast it to `AudioTrack` or `TextTrack` in order to access other properties like `codec` or `role`.

```swift
struct Events.AudioTrack {
	let current: any Trackable
}

// Notification observed specific data to consumer.
let eventData: Events.AudioTrack
if let audioTrack = eventData as? AudioTrack {
	print(audioTrack.codec)
} else {
	print("Can't access eventData.codec | audioTrack.codec \(eventData.type)")
}
```



## [Objective C Protocol | Interface](ios/objectiveC/interface.md)



## Warnings

`Protocol requirements implicitly have the same access as the protocol itself`
A clean build or changing access control made it go away - with `public, fileprivate, private`.

## Resources

[SO | pure-swift-set-with-protocol-objects](https://stackoverflow.com/questions/29278624/pure-swift-set-with-protocol-objects)

[SO | type-any-protocol-cannot-conform-to-hashable](https://stackoverflow.com/questions/74067657/type-any-protocol-cannot-conform-to-hashable)

[swift forums | mytype-does-not-conform-to-protocol-collection](https://forums.swift.org/t/how-can-i-fix-type-mytype-does-not-conform-to-protocol-collection/28802/6)
