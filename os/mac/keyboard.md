# Keyboard

Annoying things that mac os does to make the keyboard feel sluggish



## Disable Accented characters

First disable the popup showing accented characters when holding down a key.

```
defaults write -g ApplePressAndHoldEnabled -bool false
```

https://apple.stackexchange.com/questions/332769/macos-disable-popup-showing-accented-characters-when-holding-down-a-key



## Adjust Keystrokes Speed

Just select the fastest in this settings.

![](Screenshot%202023-04-13%20at%205.13.02%20PM.png)

1.  On your Mac, choose Apple menu ! > System Settings, then click Keyboard in the sidebar. (You may need to scroll down.)
    
2.  Drag the “Delay until repeat” slider on the right to set how long to wait before the character begins repeating.
    
3.  Drag the “Key repeat rate” slider on the right to set how fast characters repeat.

Source: https://support.apple.com/guide/mac-help/set-how-quickly-a-key-repeats-mchl0311bdb4/mac



## Universal Control

My Apple magic keyboard wasn't working with Shift or control / command keys.
I need to use iPad Settings app and do the following.

You have to go to `Accessibility-> Keyboards -> Full Keyboard Access` and enable it

[Good reddit PSA for universal control on mac & ipad](https://www.reddit.com/r/apple/comments/tf488r/psa_fixing_universal_control_if_it_doesnt_work/)
