


## Collapse / Fold 

To collapse all the search results in the sidebar navigator, `cmd ⌘-click` on one of the small hide/show details triangle at the beginning of the line

hold ⌘ to : close a type of warnings

hold shift & ⌘ to : close **all** types of warnings

## Behavior

### Don't show issues
On every build xcode will switch to `Issues` tab in Navigator and it becomes annoying sometimes.
To disable this behavior 
`Build` -> `Generates new issues` 
Uncheck the `show navigatior issues` checkbox.


## Keyboard



## Theme

Dracula theme for Xcode is nice.
I customized an pure black OLED theme as well.

For peer programming or presenting code, I sometimes select `Presentation` theme which quickly increases the font and then I can again revert back to my main theme configs.

## Git Config

Sometimes xcode doesn't appropriately picks up the right credentials automatically from Keychain or `.ssh` configs.
You need to explicitly run this command sometimes in order for Xcode to automatically checkout code and associate certain `public private` key pair ssh keys with specific hosts it tries to checkout.

Add the key to the Keychain with this command.
```sh
ssh-add --apple-use-keychain ~/.ssh/id_github
```

[SSH Key for Xcode Mac](https://gist.github.com/brennanMKE/8e09593ca4064deab59da807077d8f53)

## References

[maximizing-xcode-efficiency-14-tips-for-boosting-productivity](https://blog.appcircle.io/article/maximizing-xcode-efficiency-14-tips-for-boosting-productivity)
