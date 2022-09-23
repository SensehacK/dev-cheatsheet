# Map 


## Shorthands


```swift
sessionNotExpired
    .map(\.authentication.refreshToken.value)

```

Keypath - \ : shorthand for the type of `Session.Entry`
Not referencing actual Session.Entry object. Just passing a key like a dictionary key path.
Compiler infers the type using the `\.` 

`.map(Session.Entry.authentication.refreshToken.value)` doesnt compile
but `\` is saying use a reference and map internally.
 

```swift
sessionNotExpired
    .map { $0.authentication.refreshToken.value }

```




## Split

// Not present? Optional ?
        let (isSSOEnabled, isSSODisabled) = sessionEntry
            .filter { session in
                return session == nil
            }
            .mapToVoid()
            .split { _ in context.account.onlySSO }
            .map { _ in context.account.onlySSO }
            .split{$0}