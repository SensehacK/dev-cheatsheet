# Generics

## Code

```swift
func genericTrack<T>(_ type: AVMediaCharacteristic) async throws -> T? {
    switch type {
    case .audible:
        let selectedOption = try await getCurrentAVMediaSelectionOptions(.audible)
        return ATrack(id: selectedOption.displayName,
                          language: selectedOption.locale) as? T
    case .legible:
        let selectedOption = try await getCurrentAVMediaSelectionOptions(.legible)
        return BTrack(id: selectedOption.displayName,
                          language: selectedOption.locale) as? T 
    default:
        print("Error")
    }
    return nil
}
```

## References

[Generics Medium](https://navdeepsinghh.medium.com/generics-in-swift-13e792249cad)

[Apple docs](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)

[Generics Basics](https://www.swiftbysundell.com/discover/generics/)
