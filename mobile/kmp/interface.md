
## Intro

AI generated
Kotlin interfaces are blueprints for classes, outlining methods and properties that implementing classes must adhere to. They define a contract, ensuring consistency across different classes. Unlike abstract classes, Kotlin classes can implement multiple interfaces, enabling a form of multiple inheritance. Interfaces cannot store state but can declare abstract properties or provide implementations for accessors.


## Code

```kotlin
interface MyInterface {
    val myProperty: String // Abstract property
    fun myFunction() // Abstract method
    fun myDefaultFunction() { // Method with default implementation
        println("Default implementation")
    }
}

class MyClass : MyInterface {
    override val myProperty: String = "Hello"
    override fun myFunction() {
        println("Implementation of myFunction")
    }
}

val instance = MyClass()
println(instance.myProperty) // Output: Hello
instance.myFunction() // Output: Implementation of myFunction
instance.myDefaultFunction() // Output: Default implementation
```


In this example, `MyInterface` defines an abstract property `myProperty`, an abstract method `myFunction`, and a default implementation for `myDefaultFunction`. `MyClass` implements `MyInterface`, providing concrete implementations for the abstract members. Interfaces facilitate code reuse, promote decoupling, and enhance flexibility in Kotlin development.

## Documentation

[kotlin | interface](https://kotlinlang.org/docs/interfaces.html)

[jetbrains | multiplatform-expect-actual](https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-expect-actual.html)
## expect actual declaration


[SO | kmp actual expect](https://stackoverflow.com/questions/77581421/kotlin-multiplatform-expect-actual-on-interface)

