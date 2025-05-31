

## Intro

Kotlin Multiplatform (KMP)


## Project Wizard

[kotlin multiplatform wizard](https://kmp.jetbrains.com)


## Documentation

[Create your first app Kotlin | Jetbrains](https://www.jetbrains.com/help/kotlin-multiplatform-dev/compose-multiplatform-create-first-app.html)

## Gradle Build file

AI generated - Gemini

Kotlin Multiplatform (KMP) allows developers to share code across different platforms. Source sets are a key concept in KMP, defining the scope and dependencies of code intended for specific platforms or common logic. 

Source Sets in KMP

A source set is a collection of Kotlin files and resources that are compiled together. In a KMP project, there are several types of source sets:

- **commonMain**: Contains code shared across all platforms. It cannot use platform-specific APIs directly.
- **platformMain (e.g., androidMain, iosMain)**: Contains code specific to a platform. It can access platform-specific APIs and libraries.
- **Intermediate source sets (e.g., androidNativeMain)**: Shares code among a subset of targets.

When compiling for a specific target, the Kotlin compiler merges the `commonMain` source set, any relevant intermediate source sets, and the target-specific source set. 

Androidmain in KMP

`androidMain` is the source set specifically for Android-related code in a KMP project. Code placed in `androidMain` has access to Android APIs and is compiled to run on the Android platform. This allows developers to write platform-specific implementations or utilize Android-specific libraries when necessary.

Relationship and Interaction

The `commonMain` source set defines the common logic and interfaces, while `androidMain` provides the Android-specific implementations. For example, if `commonMain` declares an `expect` function to access device storage, `androidMain` would contain the `actual` implementation using Android's file system APIs.

Example

Kotlin

```
// In commonMainexpect fun getPlatformName(): String// In androidMainactual fun getPlatformName(): String {    return "Android"}
```

In this example, `getPlatformName` is declared in `commonMain` and implemented in `androidMain`. When the code is compiled for Android, the `androidMain` implementation will be used.



## Targets

A target is a part of the build responsible for compiling, testing, and packaging a piece of software aimed at one of the supported platforms. Kotlin provides targets for each platform, so you can instruct Kotlin to compile code for that specific target. Learn more about [setting up targets](https://kotlinlang.org/docs/multiplatform-discover-project.html#targets).

[kotlin lang | ref](https://kotlinlang.org/docs/multiplatform-dsl-reference.html#targets)


## Source Sets

The `sourceSets {}` block describes source sets of the project. A source set contains Kotlin source files that participate in compilations together, along with their resources, dependencies, and language settings.

A multiplatform project contains [predefined](https://kotlinlang.org/docs/multiplatform-dsl-reference.html#predefined-source-sets) source sets for its targets; developers can also create [custom](https://kotlinlang.org/docs/multiplatform-dsl-reference.html#custom-source-sets) source sets for their needs.

[kotlin lang | ref](https://kotlinlang.org/docs/multiplatform-dsl-reference.html#source-sets)