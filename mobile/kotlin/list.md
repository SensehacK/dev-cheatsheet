
## List

```kotlin
val inputChar = ('A'..'Z') + ('a'..'z') + ('0'..'9') + charRange
```

You can't append any items to the list again

Kotlin because a `List` is immutable and yours gets initialized as an empty one, so it will stay empty.

Use a `MutableList<Char>` and simply `add` single `Char`s to it if you need it

[SO | Kotlin list char](https://stackoverflow.com/questions/62671838/adding-char-to-listchar-in-kotlin)
## Mutable List


```kotlin
fun main(args: Array<String>) {
    var genList = mutableListOf<Char>()
    genList.add('a')
    genList.add('A')
    genList.add('B')
    genList.add('C')
    println(genList)
}
```
