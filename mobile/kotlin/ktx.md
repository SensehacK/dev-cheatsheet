
## Diff

To parse String to URI in Kotlin (Traditional Way )

We do

`val uri = Uri.parse(myUriString)`

and by using KTX, we can simplify above code to

```kotlin
val uri = myUriString.toUri()
```


[SO | android ktx vs normal](https://stackoverflow.com/questions/48656082/what-is-ktx-kotlin-extension-library-why-it-is-gaining-popularity-in-android)


## References


[android dev | ktx](https://android-developers.googleblog.com/2018/02/introducing-android-ktx-even-sweeter.html?m=1)
