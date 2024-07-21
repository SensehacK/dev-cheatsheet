

# Transform


Transforming data from input stream


## Map

Nuances with return result types


Type is 

```swift
typealias returnedType: Publishers
.Map<AnyPublisher<URL, Never>, Playable>?

 let results = urlOrchestrator?
            .output
            .resolvedURL
            .map { Playable(url: $0)}


```
// Compiler warning 

```error
Cannot convert value of type 'URL' to expected argument type 'Published<URL>.Publisher
```

So xcode - swift llvm compiler has hard time figuring out the return type from the `.map` closure since it could be upstream `.resolvedURL` `Published<URL>` or just `Publisher.output: URL`.

So you could get away with manually capturing value to give compiler more context. After doing this you can resort back to it since the compiler would have deduce its type automatically in its compiler cache? Don't know if it fails again if someone clones this again on a different machine. Maybe it makes the best guess at that time to either use this or that.

```swift
// 1st approach
.map { value in
   NitroPlayable(url: value)
}

// 2nd approach
.map( { Playable(url: $0)} )
```


If we do type erasure on Publisher 
`eraseToAnyPublisher`

```swift
typealias returnedType: AnyPublisher<Playable, Never>?

let results: returnedType = urlOrchestrator?
            .output
            .resolvedURL
            .map( { Playable(url: $0)} )
            .eraseToAnyPublisher()
```