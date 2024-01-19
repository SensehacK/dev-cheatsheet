


## Things to Remember

protocols can't have default implementation directly - just use extensions.
protocols can only have getters no setters.
Protocols can't have default parameters in a func. Of course remember that.
protocol variables can't be immutable

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

```error
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



## Resources

https://stackoverflow.com/questions/29278624/pure-swift-set-with-protocol-objects


https://stackoverflow.com/questions/74067657/type-any-protocol-cannot-conform-to-hashable

https://forums.swift.org/t/how-can-i-fix-type-mytype-does-not-conform-to-protocol-collection/28802/6[swift forums | mytype-does-not-conform-to-protocol-collection](https://forums.swift.org/t/how-can-i-fix-type-mytype-does-not-conform-to-protocol-collection/28802/6)
