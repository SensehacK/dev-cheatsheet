
# Either

## Intro

This is like an enum with two cases Success or Failure. Basically equivalent of result from swift or any other languagues.


## code

```kotlin
import arrow.core.Either
import arrow.core.left
import arrow.core.right

fun process(input: Int): Either<String, String> {
    return if (input > 0) {
        "Success: $input".right()
    } else {
        "Error: Invalid input".left()
    }
}
```


### fold

```kotlin
fun main() {
    val result1 = process(5)
    val unwrapped1 = result1.fold(
        { error -> "Operation failed: $error" },
        { success -> "Operation succeeded: $success" }
    )
    println(unwrapped1) // Output: Operation succeeded: Success: 5

    val result2 = process(-1)
    val unwrapped2 = result2.fold(
        { error -> "Operation failed: $error" },
        { success -> "Operation succeeded: $success" }
    )
    println(unwrapped2) // Output: Operation failed: Error: Invalid input
}
```

### getOrElse

```kotlin
fun main() {
   val result1 = process(5)
    val unwrapped1 = result1.getOrElse { "Default value" }
    println(unwrapped1) // Output: Success: 5

    val result2 = process(-1)
    val unwrapped2 = result2.getOrElse { "Default value" }
    println(unwrapped2) // Output: Default value
}
```

### when

```kotlin
fun main() {
    val result1 = process(5)
    when (result1) {
        is Either.Left -> println("Error occurred: ${result1.value}")
        is Either.Right -> println("Success: ${result1.value}")
    } // Output: Success: Success: 5

    val result2 = process(-1)
    when (result2) {
        is Either.Left -> println("Error occurred: ${result2.value}")
        is Either.Right -> println("Success: ${result2.value}")
    } // Output: Error occurred: Error: Invalid input
}
```


```kotlin
when (val result = secManagerDataSource.getDeviceIdentity()) {  
    is Either.Left -> assert(result.value.reason == 1)  
    is Either.Right -> {  
        val xact = result.value.xact  
        println(xact)  
        assert(xact.isNotBlank())  
    }  
}
```


## AI

To unwrap an `Either` in Kotlin, several approaches can be used depending on the desired outcome and the context. The `Either` type, commonly provided by libraries like Arrow, represents a value that can be either a `Left` (typically used for errors) or a `Right` (typically used for success).

Using `fold`

The `fold` function allows you to handle both the `Left` and `Right` cases in a single expression.

