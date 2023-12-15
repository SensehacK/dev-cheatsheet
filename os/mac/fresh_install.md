

Dev environment


- firefox
- google drive
- dropbox
- [xcodes app](https://github.com/XcodesOrg/XcodesApp/releases/) - multiple xcode app setup
- [iterm](https://iterm2.com/) 
- [home brew](https://brew.sh/) install
- zsh [shell brew path](fresh_install.md#brew_path) 
- [ohmyzsh](https://ohmyz.sh/#install) 
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
- [Authy](https://authy.com/download/) 
- [obsidian](https://obsidian.md/download) 
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
- [Monitor Control](https://github.com/MonitorControl/MonitorControl)
- [dracula theme](https://draculatheme.com/) everywhere iterm, xcode, vscode
-  macos quirks [keyboard](os/mac/keyboard.md)
- razer synapse not supported after mac os mojave. So use a free app called [mac mouse fix](https://mousefix.org/about/)
- [rescue Time](https://www.rescuetime.com/download) 
- mac os accessibility - zoom scroll mouse modifier
- `brew install ffmpeg`
- install youtube-dl
- install nvm - for node package manager
- [IINA video player](https://iina.io/) 
- [proxyman](https://proxyman.io/) - network sniffer 
- [Postman](https://www.postman.com/downloads/) for API prototyping 
- [Rectangle](https://rectangleapp.com/) 



## Small Caveats

### brew_path
`zsh - brew not found`
Setup home brew with your command line shell.

```bash
echo 'eval $(/opt/homebrew/bin/brew shellenv)' >> /Users/$USER/.zprofile

eval $(/opt/homebrew/bin/brew shellenv)
```



## Reinstall

MDM reinstall and Provisioning profile as well as disable remote management 

[factory reset macbook command r](https://iboysoft.com/questions/can-i-factory-reset-company-macbook-with-command-r.html)


[remote-management-when-installing-macos](https://apple.stackexchange.com/questions/311052/why-do-i-get-a-remote-management-step-when-installing-macos)

[reinstall macOS recovery mode system disk](https://forums.macrumors.com/threads/cant-reinstall-macos-from-recovery-mode-wont-allow-me-to-select-system-disk.2294294/)

Stack Overflow Exchange post copied from [this link](https://apple.stackexchange.com/questions/311052/why-do-i-get-a-remote-management-step-when-installing-macos)

```text
I believe that there's an easier way, one that does incorporate some of the steps above. Here's what worked for me:

Editing the hosts file appears to have worked **all by itself**. There's no need to reboot into Recovery Mode, disable SIP or FileVault, or move/disable the plists controlling the daemons related to device enrollment and management. You can edit the hosts file in Terminal while logged in normally, although not using those "echo" commands (even typing 'sudo echo "0.0.0.0 albert.apple.com" >> hosts' gave the error 'permission denied: hosts'). I googled editing the hosts file, and the trick appears to be to use the nano editor:

1. Type in terminal: sudo nano /private/etc/hosts. Enter admin password when prompted.
    
2. Use Arrow key on your keyboard to move the cursor to the last line and type the following lines:
    
    0.0.0.0 iprofiles.apple.com  
    0.0.0.0 mdmenrollment.apple.com  
    0.0.0.0 deviceenrollment.apple.com  
    
3. Press Control + X from keyboard to Exit.
    
4. Now you will be asked to asked whether you want to save and to enter Y for yes and N for No. Type Y [be sure to do this!]
    
5. Check to see whether the enrollment calls are being blocked by typing 'sudo profiles show -type enrollment'
    

You should see an error like this:

(34000) Error Domain=MCCloudConfigurationErrorDomain Code=34000 "The device failed to request configuration from the cloud." UserInfo={NSLocalizedDescription=The device failed to request configuration from the cloud., CloudConfigurationErrorType=CloudConfigurationFatalError}

That should be all there is to it! Many thanks to all those on gist.github.com who proposed various solutions.
```


Remove it from `Apple Business Manager` as well if you have your work laptop mac setup.

[apple discussion Docs](https://discussions.apple.com/docs/DOC-1948)
