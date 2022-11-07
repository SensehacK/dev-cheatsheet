
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

`archive -> Show in Finder -> Show package contents` 

https://stackoverflow.com/questions/7088771/iphone-where-the-dsym-file-is-located-in-crash-report?noredirect=1&lq=1

## Reference

https://medium.com/naukri-engineering/overview-of-dsym-crashlytics-in-ios-dfd72eae8b58

https://stackoverflow.com/questions/3656391/whats-the-dsym-and-how-to-use-it-ios-sdk

https://stackoverflow.com/questions/48296774/firebase-crashlytics-upload-missing-dsyms-to-see-crashes-from-1-versions-ios?noredirect=1&lq=1

https://docs.newrelic.com/docs/mobile-monitoring/new-relic-mobile-ios/configuration/retrieve-dsyms-bitcode-apps/

https://developer.apple.com/documentation/xcode/diagnosing-issues-using-crash-reports-and-device-logs