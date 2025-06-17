

# Errors

## SourceSet type mismatch

```ts
Type mismatch: inferred type is NamedDomainObjectProvider<KotlinSourceSet> but KotlinSourceSet was expected
```

For this code in gradle, the gradle build error was failing on this code inside `.gradle.build.kts`
```kotlin
val iosMain by creating {  
    dependsOn(commonMain)
}
```

```kotlin
commonMain.dependencies {
      implementation(libs.kotlinx.serialization.json)
}
```

But if I use this, it works, dont know if something's a miss or lazy initialization of build dependencies are happening in the background.
I don't know if gradle has parallelize builds & maybe the llvm / compiler is tripping up when I explicitly say dependsOn but there's not a direct value at play.

```kotlin
val commonMain by getting {
    dependencies {
		implementation(libs.kotlinx.serialization.json)
	}
}
```





## default Hierarchy template not applied


```sh
The Default Kotlin Hierarchy Template was not applied to 'project ':implementation:Auth'':
Source sets created by the following targets will clash with source sets created by the template:
[native]

Consider renaming the targets or disabling the default template by adding 
    'kotlin.mpp.applyDefaultHierarchyTemplate=false'
to your gradle.properties
```


I created a new file gradle.properties in skyAuth Implementation




## 