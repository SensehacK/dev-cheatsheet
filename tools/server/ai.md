
## IDE

Tabby is a self-hosted AI coding assistant, offering an open-source and on-premises alternative to GitHub Copilot.
[tabby github](https://github.com/TabbyML/tabby)


## Unclutter | decouple AI


### macOS 
remove apple intelligence 

You have to do some light terminal work in recovery mode:

1. Disable Apple Intelligence in System Settings.
    
2. Start up into Recovery Mode. ([Instructions](https://support.apple.com/guide/mac-help/macos-recovery-a-mac-apple-silicon-mchl82829c17/15.0/mac/15.0))
    
3. Open Disk Utility.
    
4. Right-click on 'Data' under 'Macintosh HD' and choose Mount.
    
5. Quit Disk Utility and open Terminal.
    
6. Type: rm -rf /Volumes/Data/System/Library/AssetsV2/com_apple_MobileAsset_UAF_FM_GenerativeModels
    
7. If you used the image thing, you can also remove that by typing: rm -rf /Volumes/Data/System/Library/AssetsV2/com_apple_MobileAsset_UAF_FM_Visual
    
8. Reboot
    

EDIT: 2025-08-29: Since I still get comments on it, I edited this post to be more accurate. Previously I said you have to disable SIP, but that's not the case. You can do everything you need from Recovery without disabling SIP.

[reddit source](https://www.reddit.com/r/MacOS/comments/1hca5ap/comment/m1nhv89/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button) 