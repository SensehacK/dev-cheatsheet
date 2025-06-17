


## Random String

[SO | kotlin random alphanumeric](https://stackoverflow.com/questions/46943860/idiomatic-way-to-generate-a-random-alphanumeric-string-in-kotlin)


```kotlin

fun generateChallengeCode(): String {
	val specialChars = "!\"#\$%&'()*+,-./:;<=>?@[\\]^_`{|}~"
	val charRange = specialChars.first()..specialChars.last()
	val inputChar = ('A'..'Z') + ('a'..'z') + ('0'..'9') + charRange
	val randomCode = String(CharArray(32) { inputChar.random() })
	println(randomCode)

	val encoded = Base64.Default.encode(randomCode.encodeToByteArray())
	println(encoded)
}
```