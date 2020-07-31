# Commands

This markdown file list downs all the commands for Mac OS for setting up with some configuration & statistics via Terminal.

## 

## Understanding your mac statistics

Uptime for your mac

> uptime

For checking your reboots

> last reboot

## Checking Mac Application Bundle ID

For getting the Bundle Identifier for any mac application which could be useful for bash scripting or redirecting the flow with absolute or relative paths.

Method 1 :

> osascript -e 'id of app "SomeApp"'

Method 2 :

> mdls -name kMDItemCFBundleIdentifier -r SomeApp.app

## 

