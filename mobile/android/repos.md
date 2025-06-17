

## Dependency

Adding a dependency to the project could be done using `Maven` or custom artifactory repo where your project can point to. Which is a custom tag you need to utilize.

Refer to this file [toml](toml.md), where you can add new dependency and then have it imported in your `build.gradle.kts` file. 
[gradle](gradle.md)

Three different strategies for artifact storage.
`dtm-libs-releases`: Only releases  
`dtm-libs-snapshots`: Only snapshots  
`dtm-libs`

## Nuances

In Java/Maven terms, it's like a nightly pre-release build. Multiple snapshots can be published with the same version. Artifactory will automatically version them separately with a date time + build number, but let clients still pull just from the base version (0.6.0).Releases have different rules. Only one can be published per version and then it can't (shouldn't) update.
### Error 


### Dependencies not found

```sh
:implementation:skyAuth:nativeMain: Could not resolve com.org.security.mobile:manager-android-mobile:0.4.20
Required by:
    project :implementation:orgAuth
```


Maybe this dependency is behind VPN and can't resolve it properly because of that ? 


