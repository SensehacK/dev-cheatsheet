# Commands

This markdown file list downs all the commands for Mac OS for setting up with some configuration & statistics via Terminal.

## 

## Understanding your mac statistics

Uptime for your mac

```sh
uptime
```

For checking your reboots

```sh
last reboot
```

## Keeping mac Alive

```sh
caffeinate
```


## Checking Mac Application Bundle ID

For getting the Bundle Identifier for any mac application which could be useful for bash scripting or redirecting the flow with absolute or relative paths.

Method 1 :

```sh
osascript -e 'id of app "SomeApp"'

osascript -e 'id of app "Safari"'
```

Method 2 :

```sh
mdls -name kMDItemCFBundleIdentifier -r SomeApp.app
```

## 


## Hash

MD5, sha1


```sh
openssl md5 fileName.docx
shasum -a 256 fileName.txt
shasum -a 256 /Applications/Things3.app/Contents/MacOS/Things3
```