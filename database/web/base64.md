# Base 64

## Intro

Base64 (also known as tetrasexagesimal) is a group of binary-to-text encoding

[wiki](https://en.wikipedia.org/wiki/Base64)





## Performance
concerns

> Base64 encoding causes an overhead of 33–37% relative to the size of the original binary data (33% by the encoding itself; up to 4% more by the inserted line breaks).



## Code

[kotlin lang | encode base64](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.io.encoding/-base64/)

```kt
val encoded = Base64.Default.encode("Hello, World!".encodeToByteArray())
println(encoded) // SGVsbG8sIFdvcmxkIQ==

val decoded = Base64.Default.decode(encoded)
println(decoded.decodeToString()) // Hello, World! 
```


## RFC

RFC states only support for 64 characters

So Base64 string can contain `+` and `/` , but can it cannot contain other special characters such as `$`, `|`, `'`, `*` ?



[RFC 4648 | section 4](https://www.rfc-editor.org/rfc/rfc4648#section-4) 



## Tools 

[base64 encoder](https://www.base64decode.org/)

[validator](https://base64.guru/tools/validator)
