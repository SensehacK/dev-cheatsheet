# Build for IOS Xcode project

Command for Xcode build Cordova

> ionic cordova build ios

## Issues

### Sass

if issues with sass for rebuilding x64 environment. :

> \$ npm rebuild node-sass

### Plugins

First, you should list your plugins:

> \$ cordova plugin list

Actual code for ionic:serveStatic.

> \$ "ionic:serveStatic": "export TARGET=static && ionic serve",

Dependency issues for plugin

> \$ ionic cordova plugin add folder

For adding plugin path locally.

> \$ ionic cordova plugin add /Users/kautilya/Downloads/com.kns.gx.mobile.knsrpc
> \$ ionic cordova plugin add /Users/kautilya/Downloads/com.kns.us.mobile.toolkit
> \$ ionic cordova plugin add /Users/kautilya/Downloads/com.kns.gx.mobile.knsmtc

With this result, you can simply do:

> \$ cordova plugin remove <PLUGIN_NAME>

For example:

> \$ cordova plugin remove org.apache.cordova.media

### Plugin phonegap push issue

I was able to fix by using cocoapods:1.1.1

> \# sudo gem install -n /usr/local/bin cocoapods:1.1.1
> \# sudo gem uninstall -n /usr/local/bin cocoapods # uninstall 1.2.0.beta.1
> \$ pod --version # 1.1.1
> \$ rm -rf platforms plugins
> \$ cordova platform add ios

### EA Access Permissions

Execute command

> \# sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}

It changes ownership with user(whoami) logged in for the default npm config location.

### Shared Keychain Entitlement

If the app launches shared keychain app on launch, you could check for "Shared Entitlements" - "CODE_SIGN_ENTITLEMENTS" in Xcode > Targets > Build Settings (All Combined)

Drag drop the keychain off File Explorer in Xcode.

> //:configuration = config_type
> CODE_SIGN_ENTITLEMENTS = app_name/Resources/xxxSharedKeychain.entitlements

Also if still doesn't fix your issue, you could switch to Tab "Capabilities"
Scroll down towards "Keychain Sharing"

> keychainGroup: com.Xxx.de.mobility.KeychainAccessGrp
