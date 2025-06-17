

## intro


## Code



## Intents

## work on Deeplinks

intents on android? 

https://developer.android.com/training/app-links/deep-linking



## Takeaways 


[jet brains | docs | deeplinking](https://www.jetbrains.com/help/kotlin-multiplatform-dev/compose-navigation-deep-links.html)

> For Android apps, deep link schemes are declared as intent filters in the `AndroidManifest.xml` file. See [Android documentation](https://developer.android.com/training/app-links/deep-linking?hl=en#adding-filters) to learn how to properly set up intent filters.

> - For iOS and macOS apps, deep link schemes are declared in `Info.plist` files, in the [CFBundleURLTypes](https://developer.apple.com/documentation/bundleresources/information-property-list/cfbundleurltypes) key.

## References

[reddit | question deeplinking](https://www.reddit.com/r/Kotlin/comments/1e5o89c/deeplinking_in_kotlin_compose_multiplatform_how/)

> What do you mean you don't know how to pass data into shared module?

Create some deeplink/navigation helper in common, inject it into the swift where you receive the app links callbacks from OS and just delegate them to your common helper.

And afterwards just to be creative how to subscribe your CMP UI layer to that helper. Flows will help you.

```kotlin
// Shared commonMain ApplinksHelper.kt
// Add to DI as singleton
class ApplinksHelper(
    scopes: AppCoroutineScopes
) {

    private val scope = scopes.application
    // Subscribe to this from VM or anything that will actually navigate. This exact step is out
    // of initial "how to deliver app link from iOS app to shared" scope
    private val _navigationEvents = MutableSharedFlow<NavigationRequest>(replay = 1)
    val navigationEvents: Flow<NavigationRequest> = _navigationEvents.asSharedFlow()

    fun handle(url: String) {
        scope.launch {
            _navigationEvents.emit(NavigationRequest.ToProfile)
        }
    }
}

// Shared commonMain or iosMain Koin.kt
// Utility function for iOS to get the instance from DI
fun provideApplinksHelper(): ApplinksHelper = getKoin().get()

// iOSApp.swift
u/main
struct iOSApp: App {

    var body: some Scene {
        WindowGroup {
            ContentView()
                .onOpenURL { (url) in
                    // Pass the url into Kotlin Shared world
                    KoinKt.provideApplinksHelper().handle(url: url. absoluteString)
                }
        }
    }
}
```