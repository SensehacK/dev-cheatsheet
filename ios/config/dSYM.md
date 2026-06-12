
## What it does 

Debug Symbols in Xcode & app packages.

Helps decipher memory addresses as readable part with crash analytics frameworks.

Before
```bash
//before
0   libswiftCore.dylib              0x000000018f3c9380 0x18f394000 + 217984
```

After dSYMs

```less
//after Symbolicating(dSYM is used)
0   libswiftCore.dylib              0x000000018f3c9380 closure #1 in closure #1 in closure #1 in _assertionFailure+ 217984 (_:_:file:line:flags:) + 452
```


## Location

### Xcode 

`archive -> Show in Finder -> Show package contents` 

[SO | iphone-where-the-dsym-file-is-located-in-crash-report](https://stackoverflow.com/questions/7088771/iphone-where-the-dsym-file-is-located-in-crash-report?noredirect=1&lq=1)


### Finder 

Absolute path

```sh
/Users/username/Library/Developer/Xcode/DerivedData/Project_Name-/Build/Products
```

format 

`APP_TEAM_SR_NO.app.dSYM`

### find

If you have the UUID you are looking for, you can search the files with the following command:

```sh
mdfind "com_apple_xcode_dsym_uuids == <UUID>"
```


## Config

Build Settings

Debug Information Format - `DWARF with dSYM File`


## Debug

```sh
dwarfdump CustomFramework.xcframework/ios-arm64-simulator/CustomFramework.framework/CustomFramework

dwarfdump CustomFramework.xcframework/ios-arm64/CustomFramework.framework/CustomFramework > ent_os_framework_analytics.txt
```


## Manual Key dSyms remove


```plist
<key>DebugSymbolsPath</key>
<string>dSYMs</string>
```


## Reference

[medium | overview-of-dsym-crashlytics-in-ios](https://medium.com/naukri-engineering/overview-of-dsym-crashlytics-in-ios-dfd72eae8b58)

[SO | whats-the-dsym-and-how-to-use-it-ios-sdk](https://stackoverflow.com/questions/3656391/whats-the-dsym-and-how-to-use-it-ios-sdk)

[SO | firebase-crashlytics-upload-missing-dsyms-to-see-crashes-from-1-versions-ios](https://stackoverflow.com/questions/48296774/firebase-crashlytics-upload-missing-dsyms-to-see-crashes-from-1-versions-ios?noredirect=1&lq=1)

[new-relic-mobile-ios/configuration/retrieve-dsyms-bitcode-apps/](https://docs.newrelic.com/docs/mobile-monitoring/new-relic-mobile-ios/configuration/retrieve-dsyms-bitcode-apps/)

[apple dev | diagnosing-issues-using-crash-reports-and-device-logs](https://developer.apple.com/documentation/xcode/diagnosing-issues-using-crash-reports-and-device-logs)
