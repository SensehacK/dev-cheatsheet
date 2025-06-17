
# Data Class

## Intro

In Kotlin, a `data class` is a special type of class primarily designed to hold data. By using the `data` keyword, the compiler automatically generates several useful methods, reducing boilerplate code.


## AI

Gemini

Requirements for a data class:

- The class declaration must start with the `data` keyword.
- It must have at least one parameter in the primary constructor.
- All primary constructor parameters must be declared as `val` or `var`.
- Data classes cannot be `abstract`, `open`, `sealed`, or `inner`.

Automatically generated methods:

- `equals()` and `hashCode()`: Determine object equality based on the properties in the primary constructor.
- `toString()`: Returns a string representation of the object in the format "ClassName(property1=value1, property2=value2, ...)".
- `copy()`: Creates a new object with the same properties as the original, but allows for selective property modification.
- `componentN()`: Functions that allow destructuring declarations, where N represents the position of the property in the primary constructor.

Limitations

- Data classes are designed for holding data and might not be suitable for complex logic or behavior.
- While data classes promote immutability by default using `val`, they don't enforce deep immutability for mutable properties.
- Data classes might not be ideal if inheritance or extensibility is a primary concern.



## code

### Define

```kotlin
data class User(val name: String, val age: Int)
```
```kotlin
public data class DeviceIdentityData(  
    public val xact: String,  
)
```

### Access

```kotlin
fun main() {    
	val user1 = User("Alice", 30)    
	val user2 = User("Alice", 30)   
	val user3 = user1.copy(age = 31)    
	println(user1 == user2) // true, due to auto-generated equals()    
	println(user1) // User(name=Alice, age=30), due to auto-generated toString()    
	println(user3) // User(name=Alice, age=31), using the copy() method    
	val (name, age) = user1 // Destructuring declaration using componentN()    
	println("Name: $name, Age: $age") // Name: Alice, Age: 30
}
```

