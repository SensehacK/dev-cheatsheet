
## Intro




## Difference

[SO Post diff b64 vs b64URL](https://stackoverflow.com/questions/55389211/string-based-data-encoding-base64-vs-base64url)
> The problem with Base64 is that it contains the characters `+`, `/`, and `=`, which have a reserved meaning in some filesystem names and URLs. So base64url solves this by replacing `+` with `-` and `/` with `_`. The trailing padding character `=` can be eliminated when not needed, but in a URL it would instead most likely be `%` URL encoded.


## Code

Kotlin 
```kotlin
val encoded = Base64.UrlSafe.encode("Hello? :> ".encodeToByteArray())
println(encoded) // SGVsbG8_IDo-IA== 
```


This class is not supposed to be inherited or instantiated by calling its constructor. However, predefined instances of this class are available for use. The companion object [Base64.Default](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.io.encoding/-base64/-default/index.html) is the default instance of [Base64](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.io.encoding/-base64/index.html). There are also [Base64.UrlSafe](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.io.encoding/-base64/-default/-url-safe.html) and [Base64.Mime](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.io.encoding/-base64/-default/-mime.html) instances. The padding option for all predefined instances is set to [PaddingOption.PRESENT](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.io.encoding/-base64/-padding-option/-p-r-e-s-e-n-t/index.html). New instances with different padding options can be created using the [withPadding](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.io.encoding/-base64/with-padding.html) function.

[kotlin lang | docs](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.io.encoding/-base64/)

[base64.urlSafe](https://kotlinlang.org/api/core/kotlin-stdlib/kotlin.io.encoding/-base64/-default/-url-safe.html)


## RFC



[RFC 4648 | section 5](https://www.rfc-editor.org/rfc/rfc4648#section-5) 


## Tools

https://base64.guru/standards/base64url/encode

