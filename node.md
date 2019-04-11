# Terminal commands for NPM / Node / Angular / ionic

## Installation

> \# sudo npm install -g @angular/cli
> \# sudo npm install -g ionic@latest
> \# sudo npm install
> \$ npm run ionic
> \$ npm run ionic:serveStatic

### Downgrade

> \$ npm install -g ionic@1.4.0

(version number after ionic@**\_.\_.\_**)

## NVM Version Control

~ fetch latest npm

> \$ nvm install node

To download, compile, and install the latest release of node, do this:

> \$ nvm install node

And then in any new shell just use the installed version:
nvm use node
Or you can just run it:

## Version Check

nvm run node --version

Checking versions

> \$ node -v

angular cli can report its version when you run it with the version flag

> \$ ng --version
> \$ IONIC versions
> \$ Ionic info
> \$ ionic --v

## Ionic

Set telemetry to false, No to collect analytics & data.
ionic config set -g telemetry false

Normal Way

Proper way to run an Hybrid app.
MeatPerson.

Install Node package dmg mac

Install Angular CLI

> \$ npm install -g @angular/cli

Cd to project folder

Install NPM dependencies via package json

> \$ npm install

Also give permission to folders for node installation

Finally run the static version of the project

> \$ npm run ionic:serveStatic

Build ios apps
Static build json

> \$ npm run build-static ios

dev - is dynamic

To run locally on chrome

> \$ ionic serve

## Build for IOS Xcode project

ionic cordova build ios

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

Execute command `sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}`
