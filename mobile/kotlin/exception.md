

## Checked Exception


```notes
Mychael Koelfat

11/29/2022, 3:28 PM

Hey everyone. I've gotten my Kotlin Multiplatform running on an iOS app. However, a couple seconds after running the app, it crashes, giving the error

Function doesn't have or inherit @Throws annotation and thus exceptions isn't propagated from Kotlin to Objective-C/Swift as NSError.


If I understand correctly, because Kotlin has no concept of checked exceptions, where Swift only has checked errors. Though I do not understand how I fix this, the documentation doesn't make that too clear for me. Does anyone know how to fix this?

Hylke Bron

11/29/2022, 4:06 PM

From Swift you are calling some kotlin method, that throws an exception. To fix this issue you have to do the following: • Annotate the Kotlin method with

@Throws(Throwable::class)

(or another subclass of Throwable) • Encapsulate the method call from swift with


try catch


Using this method you are converting the uncecked nature of kotlin to the checked nature of swift

Mychael Koelfat

11/29/2022, 4:30 PM

Thank you, I think I understand it now!

![kpgalligan](https://static.main.linendev.com/avatars/1a905bbc-fd5b-42c7-9683-c8824ba05d78/ee651733-41e2-4d7e-92fc-812cd3f5b027.jpg)

kpgalligan

11/29/2022, 6:17 PM

I would say that kind of depends on what you intend to do. It's happening because your kotlin code threw an exception and you didn't deal with it. If this were android, the app would crash. I generally deal with exceptions in kotlin and return some kind of error to swift, if it's an expected issue and you want to recover. You can also do "try" from Swift, but you still need to deal with it there. More of a personal preference.
```

[slack thread](https://slack-chats.kotlinlang.org/t/8012944/hey-everyone-i-ve-gotten-my-kotlin-multiplatform-running-on-)

Looks like setUnhandledExceptionHook might be what you want ? [set-unhandled-exception-hook.html#setunhandledexceptionhook](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.native/set-unhandled-exception-hook.html#setunhandledexceptionhook)