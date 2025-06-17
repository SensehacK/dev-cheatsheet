
## platform specific dependencies

```kotlin

build.Android
build.iOS

if ((extra["build.Android"] as String).toBoolean()) {  
    include(":viper-player-analytics:androidAnalytics")  
    include(":entos-ad")
}

```