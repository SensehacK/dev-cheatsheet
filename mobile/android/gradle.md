
## Install

[home brew formulae](https://formulae.brew.sh/formula/gradle)
```sh
brew install gradle
```

Usually not recommended to install gradle as a standalone executable.
Utilize `.gradlew` or `gradle.bat` script in the local project you're working on.


[gradle | installation](https://docs.gradle.org/current/userguide/installation.html)


## Getting Started

[getting started | gradle](https://docs.gradle.org/current/userguide/getting_started_eng.html)


## Commands


Cleans the whole project
```sh
gradle clean
./gradlew clean
```



Android project build

```sh
gradle build
./gradlew build
```

iOS 

```sh
gradle assembleXCFramework
```

## PATH

[CLI | docs](https://docs.gradle.org/current/userguide/command_line_interface.html)

## gradlew

[gradle wrapper](https://docs.gradle.org/current/userguide/gradle_wrapper.html)


## Sync

One thing I liked about gradle on android IDE project was it doesn't automatically tries to sync or fetch all the dependencies on app launch / IDE project open like how [SPM xcode default behavior is](ios/xcode/spm#Fetching)


## [Errors](gradle_errors.md)

## Config

# The setting is particularly useful for tweaking memory settings.  
org.gradle.jvmargs=-Xmx2048m -Dfile.encoding=UTF-8



Root of the gradle (whole project)
