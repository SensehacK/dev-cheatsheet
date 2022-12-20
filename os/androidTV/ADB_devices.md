
Services to be turned on for Accessibility options


## Setup ADB

On Mac OS

# Manually (just the platform tools)

This is the easiest way to get a manual installation of ADB and Fastboot.

1.  Delete your old installation _(optional)_
    
    ```bash
     rm -rf ~/.android-sdk-macosx/
    ```
    
2.  Navigate to [https://developer.android.com/studio/releases/platform-tools.html](https://developer.android.com/studio/releases/platform-tools.html) and click on the `SDK Platform-Tools for Mac` link.
    
3.  Go to your Downloads folder
    
    ```javascript
     cd ~/Downloads/
    ```
    
4.  Unzip the tools you downloaded
    
    ```python
     unzip platform-tools-latest*.zip 
    ```
    
5.  Move them somewhere you won't accidentally delete them
    
    ```bash
     mkdir ~/.android-sdk-macosx
     mv platform-tools/ ~/.android-sdk-macosx/platform-tools
    ```
    
6.  Add `platform-tools` to your path
    
    ```bash
     echo 'export PATH=$PATH:~/.android-sdk-macosx/platform-tools/' >> ~/.zshrc
    ```
    
7.  Refresh your bash profile (or restart your terminal app)
    
    ```bash
     source ~/.zshrc
    ```
    
8.  Start using adb
   ```bash
     adb devices
    ```


https://stackoverflow.com/questions/17901692/set-up-adb-on-mac-os-x?rq=1



## Setup Wireless



https://www.makeuseof.com/use-adb-over-wifi-android/

https://www.makeuseof.com/how-to-use-adb-on-android-tv/

TV Actions Pro

```bash
adb shell settings put secure enabled_accessibility services dev.vodik7.tvquickactions


adb shell pm grant dev.vodik7.tvquickactions android.permission.WRITE_SECURE_SETTINGS
```

Button Remapper

```bash
adb shell settings put secure enabled_accessibility services dev.vodik7.tvquickactions


adb shell pm grant dev.vodik7.tvquickactions android.permission.WRITE_SECURE_SETTINGS
```


## Sideload app



https://www.xda-developers.com/how-to-sideload-apps-android-tv/