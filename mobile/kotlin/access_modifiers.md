
## kotlin lib 

need to specify `explicit` visibility modifier


```kotlin
public val authState: Flow<AuthState>  
    get() = authKmp.authStateF
    
private lateinit var authKmp: AuthClient
```


## app


Default is `public` if you dont provide any

```kotlin
val authState: Flow<AuthState>  
    get() = authKmp.authStateF
```

## Deeplink


[swift | access_control](ios/swift/access_control.md)
