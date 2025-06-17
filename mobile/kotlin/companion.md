

##  Intro

Companion objects allow you to define class-level functions and properties. This makes it easy to create factory methods, hold constants, and access shared utilities.




## Code

```kotlin
class User(val name: String) {
    // Defines a companion object that acts as a factory for creating User instances
    companion object Factory {
        fun create(name: String): User = User(name)
    }
}

fun main(){
    // Calls the companion object's factory method using the class name as the qualifier. 
    // Creates a new User instance
    val userInstance = User.create("John Doe")
    println(userInstance.name)
    // John Doe
}
```


So `companion object` basically just means the methods are static
So I guess you could call   `User.Factory.create` but `User.create` is exposed

## Reference

[Kotlin lang | companion](https://kotlinlang.org/docs/object-declarations.html#companion-objects)