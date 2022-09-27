# Keyboard 


Have keymap bindings like mac on windows.

## Switch Alt - Ctrl Mac

Install the app "SharpKeys" for overwriting the Registry Editor in Windows 10. Its 2020 and we still don't have a proper settings to override the default keymaps on Windows. Registry is a mess and we have to utilize an utility just to overwrite some bunch of hex / other encoded values to map the keys. Switching back from Mac OS to Windows for development machine is a pain in the butt!

Use the sync settings from this [link](https://github.com/SensehacK/sense-setup) in windows folder.

Now we have officially switched the Alt - ctrl buttons according to Mac OS.

## Alt Tab Caveat

So when we map ctrl - alt, turns out alt - tab is used in Windows to switch apps and mac OS uses command - tab.  
So Windows emphasizes Ctrl everywhere but for switching apps they chose "Alt" DAMN! **insert Kendrick Lamar album cover**

So we would add one more script to rectify this issue using the holy grail of automation scripting on Windows. The one and only "[AutoHotkey](https://www.autohotkey.com/)"

After installation, just create a new Autohotkey script and add the following content towards it! [Source](https://superuser.com/questions/543971/how-to-change-the-windows-alttab-hotkey-to-something-else/543975)

> LControl & Tab::AltTab

If you need to download that script FYI [link](https://github.com/SensehacK/sense-setup) in windows folder.



## Keyboard input

Lag for keyboard input on windows for repeating keys.
Used this panel to fix it.
https://www.makeuseof.com/windows-10-fix-keyboard-lag/