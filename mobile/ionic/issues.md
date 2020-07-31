# Issues

## Issues

### Sass

if issues with sass for rebuilding x64 environment. :

> $ npm rebuild node-sass

### Plugins

First, you should list your plugins:

> $ cordova plugin list

Actual code for ionic:serveStatic.

> $ "ionic:serveStatic": "export TARGET=static && ionic serve",

Dependency issues for plugin

> $ ionic cordova plugin add folder

For adding plugin path locally.

> $ ionic cordova plugin add /Users/kautilya/Downloads/com.kns.gx.mobile.knsrpc $ ionic cordova plugin add /Users/kautilya/Downloads/com.kns.us.mobile.toolkit $ ionic cordova plugin add /Users/kautilya/Downloads/com.kns.gx.mobile.knsmtc

With this result, you can simply do:

> $ cordova plugin remove

For example:

> $ cordova plugin remove org.apache.cordova.media

### Plugin phonegap push issue

I was able to fix by using cocoapods:1.1.1

> \# sudo gem install -n /usr/local/bin cocoapods:1.1.1 \# sudo gem uninstall -n /usr/local/bin cocoapods \# uninstall 1.2.0.beta.1 $ pod --version \# 1.1.1 $ rm -rf platforms plugins $ cordova platform add ios

### EA Access Permissions

Execute command

> \# sudo chown -R $\(whoami\) $\(npm config get prefix\)/{lib/node\_modules,bin,share}

It changes ownership with user\(whoami\) logged in for the default npm config location.

### Shared Keychain Entitlement

If the app launches shared keychain app on launch, you could check for "Shared Entitlements" - "CODE\_SIGN\_ENTITLEMENTS" in Xcode &gt; Targets &gt; Build Settings \(All Combined\)

Drag drop the keychain off File Explorer in Xcode.

> //:configuration = config\_type CODE\_SIGN\_ENTITLEMENTS = app\_name/Resources/xxxSharedKeychain.entitlements

Also if still doesn't fix your issue, you could switch to Tab "Capabilities" Scroll down towards "Keychain Sharing"

> keychainGroup: com.Xxx.de.mobility.KeychainAccessGrp

### Shared Keychain Entitlement

If you get blank screen at launch with ionic app. As for me I just executed the command

> ionic cordova platform add ios

But forgot the build command

> ionic cordova build ios

```text
ERROR: Start Page at 'www/index.html' was not found.
2019-12-10 22:09:35.171363-0500 MyApp[2706:762104] ERROR Internal navigation rejected - <allow-navigation> not set for url='about:blank'
```

### Authored by : [Kautilya Save](https://sensehack.github.io/)

### [GitHub](https://github.com/SensehacK)

