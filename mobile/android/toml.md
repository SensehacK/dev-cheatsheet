

## Dependency format

`libs.versions.toml`
```toml
sec-manager-android = "0.5.4"
secmanager = { group = "com.comcast.dtm.mobile", name = "secmanager-android-mobile", version.ref = "sec-manager-android" }  
secmanager-google = { group = "com.comcast.dtm.mobile", name = "secmanager-android-mobile", version.ref = "sec-manager-android" }
```

utilize them in gradle file

Turns out you need to not use `-` when you're trying to inject or use it.
You have to use `.`

`build.gradle.kts`

```kotlin
kotlin {
sourceSets {
	val commonMain by getting {  
	    dependencies { 
		    // this doesn't work
			// implementation(libs.secmanager-android)
			// But this works
			implementation(libs.secmanager)
            implementation(libs.secmanager.google)
		}
	}
}
}
```

## Bundles

When you want to group your library dependencies into a bundle, you can utilize this format.

```toml
custom-sdk-lib = { group = "com.org.custom.sdk", name = "custom-sdk-lib", version.ref = "custom-sdk-lib" }
custom-sdk-okhttp = { group = "com.org.custom.sdk", name = "custom-sdk-okhttp", version.ref = "custom-sdk-okhttp" }
custom-sdk-shared-preferences = { group = "com.org.custom.sdk", name = "custom-sdk-shared-preferences", version.ref = "custom-sdk-shared-preferences" }

custom-sdk = [
    "custom-sdk-lib",
    "custom-sdk-okhttp",
    "custom-sdk-shared-preferences"
]
```

Usage in gradle.kt

```kotlin
implementation(libs.bundles.custom.sdk)
// vs
implementation(libs.custom.sdk.lib)
```