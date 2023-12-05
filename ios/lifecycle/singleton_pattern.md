## Singleton Builder Pattern

```swift
class MySingleton {

    static let shared = MySingleton()
    
    struct Config {
        let param:String
    }
    private static var config:Config?
    
    class func setup(_ config:Config){
        MySingleton.config = config
    }
    
    private init() {
        guard let config = MySingleton.config else {
            fatalError("Error - you must call setup before accessing MySingleton.shared")
        }
        
        //Regular initialisation using config
    }
}
```

Init

```swift
MySingleton.setup(MySingleton.Config(param: "Some Param"))
```

Access Singleton

```swift
MySingleton.shared
```

[SO source](https://stackoverflow.com/questions/28429544/singleton-and-init-with-parameter)