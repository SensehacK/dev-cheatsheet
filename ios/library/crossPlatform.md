
# Cross Platform

## Javascript Core

[nshipster | javascriptcore](https://nshipster.com/javascriptcore/)

[javascriptcore-and-swift/](https://www.andyibanez.com/posts/javascriptcore-and-swift/)

[javascriptcore-the-holy-grail-of-cross-platform](https://www.lucidchart.com/techblog/2018/02/14/javascriptcore-the-holy-grail-of-cross-platform/)

[apple dev | javascriptcore](https://developer.apple.com/documentation/javascriptcore)

## Kotlin Multi Platform

[Kotlin multiplatform get-started](https://kotlinlang.org/docs/multiplatform.html#get-started)

[iOS packaging](https://kotlinlang.org/docs/multiplatform-build-native-binaries.html#build-universal-frameworks)

iOS `iosArm64` still isn't in Tier 1 but [hopefully it gets added](https://kotlinlang.org/docs/native-target-support.html#tier-2).

By default, an Objective-C framework produced by Kotlin/Native supports only one platform.
However, you can merge such frameworks into a single universal (fat) binary using the `lipo tool`.
This operation especially makes sense for 32-bit and 64-bit iOS frameworks. 
In this case, you can use the resulting universal framework on both 32-bit and 64-bit devices.
