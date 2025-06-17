

## Code



```kotlin

val mapOfStringDict = mapOf(        "key1" to mapOf("nestedKey1" to "value1", "nestedKey2" to "value2"),        "key2" to mapOf("nestedKey3" to "value3", "nestedKey4" to "value4")    )

mapOfStringDict.forEach { (key, value) ->        
	println("$key: $value")    
}
```


## Get Key Value 


```kotlin
val map = mapOf("apple" to 1, "banana" to 2, "cherry" to 3)

// Using get() method
val value1 = map.get("apple") // value1 will be 1
val value4 = map.get("grape") // value4 will be null because "grape" is not a key

// Using [] operator
val value2 = map["banana"] // value2 will be 2
val value5 = map["grape"] // value5 will be null because "grape" is not a key
```