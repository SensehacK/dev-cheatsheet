

## Description

[santa | google](https://github.com/northpolesec/santa)
A binary authorization and monitoring system for macOS

[Example profile with property list](https://github.com/northpolesec/santa/blob/main/docs/deployment/com.northpolesec.santa.example.mobileconfig#L45)

How to add binaries to the property list

[rules object | documentation](https://northpole.dev/development/sync-protocol.html#ruledownload-response)


```sh
santactl status
```

## Why

You can disable your installed apps to not run in the background,

## Block apps

```sh
shasum -a 256 /Applications/Things3.app/Contents/MacOS/Things3
```


identifier
The attribute of the binary the rule should match on e.g. the signing ID, team ID, or CDHash of a binary or sha256 hash value


```plist
<dict>
<key>identifier</key
<string>e9f5c61a4aafbbdf70f09af5915b674477191b540ff7786cc1e9766f7565a64b</string>
<key>policy</key>
<string>BLOCKLIST</string>
<key>rule_type</key>
<string>BINARY</string>
</dict>
```