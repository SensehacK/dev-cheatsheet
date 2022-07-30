# Disable Gatekeeper

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


> sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder

For Mac OS Catalina 10.15.6
