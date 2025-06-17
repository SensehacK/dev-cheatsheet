

## Code


```kotlin
public sealed class AuthState {  
    /** First time initialized flow. */  
    public data object UNKNOWN : AuthState()  
    /** Logged in with appropriate JWT generation but not provisioned */  
    public data object UNINITIALIZED : AuthState()  
    /** Device has been activated with security DRM */  
    public data object PROVISIONED : AuthState()  
}
```

vs 

```kotlin
enum class DeviceState {
    Unprovisioned,
    Provisioned,
}
```


## Enum vs Sealed

Copied off  [SO | enum vs sealed](https://stackoverflow.com/a/65226315/5177704)

In enum classes, each enum value cannot have its own unique property. You are forced to have the same property for each enum value:
```kotlin
enum class DeliveryStatus(val trackingId: String?) {
    PREPARING(null),
    DISPATCHED("27211"),
    DELIVERED("27211"),
}
```
Here we need the `trackingId` only for the `DISPATCHED` and `DELIVERED`, the `PREPARING` is forced to have a `null` value.


In case of sealed classes, we can have different properties for each subtype:
```kotlin
sealed class DeliveryStatus
class Preparing() : DeliveryStatus()
class Dispatched(val trackingId: String) : DeliveryStatus()
class Delivered(val trackingId: String, val receiversName: String) : DeliveryStatus()
```

Here we have different properties for each subtype. `Preparing` doesn't need properties for our use case, so we have the flexibility to not specify any property unlike forced `null` values in enums. `Dispatched` has one property while the `Delivered` has two properties.


Tl;dr I think its about heterogenous data in the associated values of sealed class vs enum class.





## Switch

```kotlin
val authS = AuthState.unknown
when (authS){  
    AuthState.UNKNOWN -> initialLoginRoute()  
  
    AuthState.UNINITIALIZED -> uninitializedLoginFlow()  
  
    AuthState.PROVISIONED -> provisionedFlow()  
}
```


## if else 

```kotlin
fun handleProvisioning(result: AuthState) {
    when (result) {
        is Result.PROVISIONED -> println("Provisioned: ${result.data}")
        else -> println("Not provisioned")
    }
}
```

## Mind Map

[swift | enum](ios/swift/enum.md)