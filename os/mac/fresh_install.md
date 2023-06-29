

Dev environment


- firefox
- google drive
- dropbox
- [xcodes app](https://github.com/XcodesOrg/XcodesApp/releases/) - multiple xcode app setup
- [iterm](https://iterm2.com/) 
- home brew install  (https://brew.sh/)
- zsh [shell brew path](fresh_install.md#brew_path)
- rosetta install
- bartender app
- be focused pro - pomodoro app
- github desktop
- vscode
- 
- Things app
- fantastical app 2 (microsoft outlook personal requires app password not traditional password)
- istats pro
- 1password
- Authy https://authy.com/download/
- obsidian https://obsidian.md/download
- screenshots directory location
- cocoapods
- finder enhancements ( file extensions, [hidden_files](hidden_files.md), folders on top, search current folder, disable tags, disable cloud in sidebar, default home location)
- spark (all emails)
- xcode 2 more simulators (one latest, another 2 or 1 year older)
- xcode workspace config
- disable spotlight & key
- alfred snippets - dropbox sync
- Keyboard macros (Keychron Via)
- video conferencing tools
- External displays same 
- Monitor Control (https://github.com/MonitorControl/MonitorControl)
- [dracula theme](https://draculatheme.com/) everywhere iterm, xcode, vscode
-  macos quirks [keyboard](os/mac/keyboard.md)
- razer synapse not supported after mac os mojave. So use a free app called [mac mouse fix](https://mousefix.org/about/)
- [rescue Time](https://www.rescuetime.com/download) 
- mac os accessibility - zoom scroll mouse modifier
- `brew install ffmpeg`
- install youtube-dl
- install nvm - for node package manager
- IINA https://iina.io/
- proxyman - network sniffer https://proxyman.io/
- Postman for API prototyping https://www.postman.com/downloads/
- Rectangle https://rectangleapp.com/



## Small Caveats

### brew_path
`zsh - brew not found`
Setup home brew with your command line shell.

```bash
echo 'eval $(/opt/homebrew/bin/brew shellenv)' >> /Users/$USER/.zprofile

eval $(/opt/homebrew/bin/brew shellenv)
```