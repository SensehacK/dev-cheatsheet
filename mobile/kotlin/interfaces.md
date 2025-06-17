
## Intro

In Kotlin, an interface is a blueprint for classes, defining a set of methods that classes implementing the interface must provide implementations for. Interfaces can also include default implementations for methods, and properties, but they cannot hold state. They are defined using the `interface` keyword.

## Desc


Interfaces are equivalent of protocols in swift. Or Interface in java.

```kt
interface Printable {
    val content: String
    fun print(): String
}
```

## Anonymous objects

You can create direct extension as a default implementation of Interface / protocol in kotlin.

```kt
val sentence = object : Printable {
    override val content: String = "A beautiful sentence."
    override fun print(): String = "[Print Result]\n$content"
}
```


[Create anonymous objects](https://www.baeldung.com/kotlin/anonymous-objects)