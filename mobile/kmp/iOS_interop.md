# Apple Interoperation

## Intro

The whole point of using KMP is to write less redundant code on each platform. So in this document we can see how to integrate with apple ecosystem or iOS specific implementation.

## Documentation

[kotlin | ios integration methods](https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-ios-integration-overview.html)

[kotlin | native obj-c interop](https://kotlinlang.org/docs/native-objc-interop.html)

## Integrations

### Plugins

Add Kotlin KMP plugins in android studio IDE
- Kotlin Multiplatform 
- Compose Kotlin Multiplatform



### gradle Build 

Run the build command in Android studio embedded terminal to build the artifacts for KMP lib for iOS xcode.
It can take 2 - 5 mins depending on the size of the project / hardware.

```sh
./gradlew :proj_directory:lib_name:embedAndSignAppleFrameworkForXcode
```


### gradle tasks

You can have tasks available to u.
eg. unit tests / xcode specific ? or platform specific

```sh
./gradlew tasks

// -- list (quick MAN page)
```

## Files

`build.gradle.kts` - Current library gradle build settings
`gradle.properties` - Current project gradle properties
`.xcodeproj` - xcode | iOS specific [build](ios/xcode/build.md) project file format 
`Package.swift` - SPM package - swift package manager [spm](spm.md) dependency format


## iOS Build

### gradle properties

iOS specific project
Need to update `gradle.properties`

```json
#Targets to build:  
build.Android=true  
build.iOS=true  // iOS Specific
build.browser=false  
build.native=false
```

[jetbrains | multiplatform-integrate-in-existing-app](https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-integrate-in-existing-app.html)

### run iOS app config

You need to add the iOS configuration to the android project.
You need to provide `.xcproj` since `.xcworkspace` was having issues getting the UI scheme to be visible and linkable.
It takes a good minute to resolve those references of xcode proj inside of Android studio config dialog box.




## Custom apple dependencies

You can utilize your own apple `.xcframework` in Android KMP project

> You can also reuse other libraries and frameworks from the iOS ecosystem in your iOS source sets. Kotlin supports interoperability with Objective-C dependencies and Swift dependencies if their APIs are exported to Objective-C with the `@objc` attribute. Pure Swift dependencies are not yet supported.


Probably using `cinterop` 

> You can use the cinterop tool to create Kotlin bindings for Objective-C or Swift declarations. This will allow you to call them from the Kotlin code.

[kotlin KMP | iOS dependencies framework dependency](https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-ios-dependencies.html#with-cinterop)

Two variants of using `cinterop` or else you would have to utilize [cocoapods](cocoapods.md)

### Library mode

```kotlin
kotlin {
    iosArm64() {
        compilations.getByName("main") {
            val DateTools by cinterops.creating {
                // Path to the .def file
                definitionFile.set(project.file("src/nativeInterop/cinterop/DateTools.def"))

                // Directories for header search (an analogue of the -I<path> compiler option)
                includeDirs("include/this/directory", "path/to/another/directory")
            }
            val anotherInterop by cinterops.creating { /* ... */ }
        }

        binaries.all {
            // Linker options required to link to the library.
            linkerOpts("-L/path/to/library/binaries", "-lbinaryname")
        }
    }
}
```


### framework mode

```kotlin
kotlin {
    iosArm64() {
        compilations.getByName("main") {
            val DateTools by cinterops.creating {
                // Path to the .def file
                definitionFile.set(project.file("src/nativeInterop/cinterop/DateTools.def"))

                compilerOpts("-framework", "MyFramework", "-F/path/to/framework/")
            }
            val anotherInterop by cinterops.creating { /* ... */ }
        }

        binaries.all {
            // Tell the linker where the framework is located.
            linkerOpts("-framework", "MyFramework", "-F/path/to/framework/")
        }
   }
}
```


## Singletons

[objc-interop | kotlin](https://kotlinlang.org/docs/native-objc-interop.html#kotlin-singletons)


## Documentation

```kotlin
kotlin {
	targets.withType<org.jetbrains.kotlin.gradle.plugin.mpp.KotlinNativeTarget> {
	compilations.get("main").compilerOptions.options.freeCompilerArgs.add("-Xexport-kdoc")
	    }
}
```

[kdoc migration to iOS swift / objc](https://kotlinlang.org/docs/native-objc-interop.html#provide-documentation-with-kdoc-comments)

> The ability to export KDoc comments to generated Objective-C headers is [Experimental](https://kotlinlang.org/docs/components-stability.html). It may be dropped or changed at any time. Opt-in is required (see the details below), and you should use it only for evaluation purposes. We would appreciate your feedback on it in [YouTrack](https://youtrack.jetbrains.com/issue/KT-38600).


## Limitation

Still generates on Obj-C header [type sh!t](https://open.spotify.com/track/28drn6tQo95MRvO0jQEo5C?si=29e9e6c6774443ca)

[swift-interopedia](https://github.com/kotlin-hands-on/kotlin-swift-interopedia/blob/main/docs/classesandinterfaces/Data%20classes.md) re: data classes -> structs

## Data Conversions

Byte array to NS Data 

[github gist](https://gist.github.com/noahsark769/61cfb7a8b7231e2069a9dab94cf74a62)
```kotlin
import kotlinx.cinterop.memScoped
import kotlinx.cinterop.allocArrayOf
import kotlinx.cinterop.addressOf
import kotlinx.cinterop.usePinned
import platform.Foundation.NSData
import platform.Foundation.create
import platform.posix.memcpy

public fun ByteArray.toData(): NSData = memScoped {
    NSData.create(bytes = allocArrayOf(this@toData),
        length = this@toData.size.toULong())
}

public fun NSData.toByteArray(): ByteArray = ByteArray(this@toByteArray.length.toInt()).apply {
    usePinned {
        memcpy(it.addressOf(0), this@toByteArray.bytes, this@toByteArray.length)
    }
}
```


## Code conversions

Additionally, SKIE renames cases that collide with Swift keywords and Objective-C methods. Kotlin also does this, but its implementation is not correct in some cases, which creates a difference in some situations. For example:

### Obj-C

Note that the names that collide with Obj-C methods are renamed by adding the `the` prefix, instead of the `_` suffix. So, for example, `zone` becomes `theZone`.


### Swift 
Kotlin (but not SKIE) renames `return` to `return_`, which is unnecessary because `return` is only a soft keyword in Swift.

Swift methods get the `_return` instead of just the `return`

[enum naming_conventions | touchlabs](https://skie.touchlab.co/features/enums)


## Reactive

Flows -> Combine

```gradle
skie { features 
		{ enableFlowCombineConvertorPreview = true }
}
```

```kotlin
fun helloWorld(): Flow<String> { } 
```

```swift
let publisher = helloWorld().toPublisher()
publisher.sink { $0 }
```

[SKIE | combine](https://skie.touchlab.co/features/combine)


## Async

[SKE | suspend | await](https://skie.touchlab.co/features/suspend)

## Direct Integration

### Direct Integration

local integration method 


[multiplatform-direct-integration](https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-direct-integration.html)


build script

```sh
cd "$SRCROOT/.."
./gradlew :shared:embedAndSignAppleFrameworkForXcode
```

Need to update `shared` to either sky-auth ? or nitro-apple
```sh
cd "$SRCROOT"
# need this coz of the way of the project being structured here
cd ../..
# Runs the actual gradle command which builds the module / lib for 
# xcode to sign or integrate into the project scheme
./gradlew :implementation:skyAuth:embedAndSignAppleFrameworkForXcode
```


Doc for iOS specific.
[make-your-cross-platform-application-work-on-ios](https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-integrate-in-existing-app.html#make-your-cross-platform-application-work-on-ios)

### export package

[SPM | kmp support](https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-spm-export.html)


### errors

If the build isn't succeeding in android studio locally on the IDE, you can try doing clean & gradle build

Disable JS builds in `gradle.properties` by setting `build.browser=false`

```sh 
- Run `./gradlew common:assemble`
- Run `./gradlew common:publishToMavenLocal`
```


### task not found

[SO | KMM: embedAndSignAppleFrameworkForXcode task not found](https://stackoverflow.com/questions/69928979/kmm-embedandsignappleframeworkforxcode-task-not-found) 

I think embedAndSignAppleFrameworkForXcode is not supposed to run from the terminal as packForXCode used be.

The proper way to run this task is from XCode build system.

Anyway, I was able to run embedAndSignAppleFrameworkForXcode from terminal after exporting the following variables.

```kotlin
export CONFIGURATION\=Debug
export ARCHS\=x86_64
export EXPANDED_CODE_SIGN_IDENTITY\=-
export FRAMEWORKS_FOLDER_PATH\=iosApp.app/Frameworks
export SDK_NAME\=iphonesimulator15.0
export TARGET_BUILD_DIR\="../build/ios/${CONFIGURATION}-iphonesimulator"
```



## Manual Integration


### Xcode search paths

I needed to add `/$(CONFIGURATION)/$(SDK_NAME)` and make it as non-recursive. Now even if I run app on simulator and then on actual device, Xcode maps & links correct shared.framework. This solved my issue.

That setting is available inside `xcodeproj` 
`Targets -> Build Settings -> Framework Sarch Paths`

[SO | linking issue with kmp iOS](https://stackoverflow.com/questions/74347353/kotlin-multiplatform-ios-integration-issue-in-linking-shared-framework-for-resp)


## iOS KMP resources

[kmp resources for ios dev by touchlab](https://touchlab.co/iosdevex)


[kmp ios ideal setup guide](https://touchlab.co/ideal-ios-kmp-setup)


Enable “experimental Multiplatform IDE feature” on android studio settings

You will see the Debug icon enabled when iOSApp is selected, but you can only debug Kotlin Code (better than xcode-kotlin).
[slack chat](https://slack-chats.kotlinlang.org/t/27056583/how-can-i-attach-debugger-to-the-ios-app-through-android-stu)

[medium | inspect kmms kotlin code on xcode](https://medium.com/@uwaisalqadri/inspect-kmms-kotlin-code-directly-from-xcode-a5f66bb7c864)

