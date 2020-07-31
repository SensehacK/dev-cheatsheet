# Commands

This markdown file list downs all the commands for Mac OS for setting up with some configuration & statistics via Terminal.

## Enable Hidden files

The Quickest Way to Show/Hide Hidden Files Since the release of macOS Sierra, when in Finder, it is now possible to use the shortcut: CMD + SHIFT + .

Enable hidden files on Mac OS

> $ defaults write com.apple.finder AppleShowAllFiles YES

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

## Disable Mac OS Mojave Gatekeeper

It a simple fix and here is how we fix it: Open the Terminal app from the /Applications/Utilities/ folder and then enter the following command syntax:

### Disable

Option I For a certain application run in Terminal:

> sudo xattr -rd com.apple.quarantine /Applications/LockedApp.app

Option II To disable checks globally run in Terminal:

> sudo spctl --master-disable

### Re enable

To re-enable Gatekeeper simply run the following command in the Terminal app

> sudo spctl --master-enable

### Host DNS Restart

This command will restart the DNS of the system if you have made changes to Mac “etc/hosts” file.

> sudo killall -HUP mDNSResponder

Works in Mac OS Mojave 10.14.6

