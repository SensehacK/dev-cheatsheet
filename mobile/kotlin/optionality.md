# Optionality

## Intro

Optional values which can be null or have a value. Determined at runtime or compile time


## Code


```kotlin
fun myFunction(name: String? = null) {
    val displayName = name ?: "defaultName"
    println("Name: $displayName")
}

fun main() {
    myFunction() // Output: Name: defaultName
    myFunction("Bob") // Output: Name: Bob
    myFunction(null) // Output: Name: defaultName
}
```

### Check optionality


Do if true || not null
```kotlin
fun processNullableString(text: String?) {
    // Safe call operator: executes the lambda only if 'text' is not null
    text?.let {
        println("The text is: $it")
    }
```


### if else
if else statement? 

```kotlin
fun processNullableString(text: String?) {
    if (text != null) {
        // 'text' is not null, safe to use it directly
        println("The text is: $text")
        // Perform operations on 'text'
    } else {
        // 'text' is null
        println("The text is null")
        // Handle the case where 'text' is null
    }
}
```

### if let 

If let equivalent in kotlin `?. let { } ?: run { }`
[swift counterpart](ios/swift/optionals#If%20Let)

```kotlin
fun process(text: String?) {
    text?.let {
        // Code to execute if text is not null
        println("Text is not null: $it")
    } ?: run {
        // Code to execute if text is null (else block)
        println("Text is null")
    }
}
```

### Default value

```kotlin
var name: String? = null
val defaultName = name ?: "Sensehack"
println(defaultName)

name = "Kay"
val assignedName = name ?: "Kautilya"

println(assignedName)
```


## Mind Map

Swift counterpart [Optionals](/ios/swift/optionals.md)

## If let optional


One option is to use a [safe cast operator](https://kotlinlang.org/docs/reference/typecasts.html#safe-nullable-cast-operator) + [safe call](https://kotlinlang.org/docs/reference/null-safety.html#safe-calls) + [`let`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/let.html):

```kotlin
(getUser() as? User)?.let { user ->
    ...
}
```

Another would be to use a [smart cast](https://kotlinlang.org/docs/reference/typecasts.html#smart-casts) inside the lambda passed to `let`:

```kotlin
getUser().let { user ->
    if (user is User) {
        ...
    }
}
```

But maybe the most readable would be to just introduce a variable and use a smart cast right there:

```kotlin
val user = getUser()
if (user is User) {
    ...
}
```

[Reference | SO post](https://stackoverflow.com/questions/44236842/kotlin-equivalence-to-swifts-combination-of-if-let-cast)


## also 

In Kotlin, `also` is a scope function that operates on an object and returns the object itself after executing a block of code. It's useful for performing side effects or additional operations on an object without modifying it or interrupting method chaining. The object is referenced within the `also` block using `it` (by default) or a custom name if specified.

```kotlin
fun main() {
    val numbers = mutableListOf(1, 2, 3)
    val result = numbers.also {
        println("Original list: $it") // Prints: Original list: [1, 2, 3]
        it.add(4)
    }
    println("Modified list: $result") // Prints: Modified list: [1, 2, 3, 4]
}
```


## swift guard


```swift
guard let e = email.text , !e.isEmpty else { return }
```
[guard](guard.md)

```kotlin
val e = email.text?.let { it } ?: return
```


## if let 

[swift equivalent](ios/swift/optionals#If%20Let)

```kotlin
val a = b?.let {  
    // If b is not null.  
} ?: run {  
    // If b is null.  
}
```

## let 


In Kotlin, the `let` function's return type defaults to `Unit` if the lambda expression within it does not explicitly return a value. `Unit` is Kotlin's equivalent of `void` in Java, signifying that a function does not return a meaningful value.

When a `let` block's last expression is a statement that doesn't produce a value (like a variable assignment or a `for` loop without a `return`), the `let` function implicitly returns `Unit`. However, if the lambda contains an expression that yields a value, that value becomes the return value of the `let` function.

```kotlin
suspend fun openInBrowser(url: String): Pair<Boolean, LoginData?>  {
val loginData = callbackData?.let {  
    println("Successful callback!")  
    it  
} ?: run {  
    println("Failure in authenticating with user credentials")  
    return Pair(false, null)  
}
}
```