# WSL

## Open in Linux subsystem

I'm on Windows 10 Home with May Update and have Ubunto 18.04 for WSL installed, I can open the console in any folder with Shift + Right Click and selecting the Open Linux shell here option

> Shift + Right Click -&gt; Open Linux shell

[Source](https://stackoverflow.com/questions/49526259/start-wsl-ubuntu-in-specific-or-current-folder-on-windows)

## Command Line

Open in your designated file path and run the command

> ubuntu run

Which will open the ubuntu WSL in that specific folder.

## WSL to Windows

If you're in specific file path and you just need to view that directory or workspace in GUI.

You could utilize this command and it will directly open up the $pwd path in your file explorer.

> explorer.exe .

[Source](https://www.howtogeek.com/426749/how-to-access-your-linux-wsl-files-in-windows-10/)

Or if you need VS Code to open up a project.

> code .

## Windows Path

You can set path on default shell

By this I can open a specific $pwd in explorer to view it So when we enter ```open .`` it would internally convert that syntax to```explorer.exe .\`\` Pretty sweet Window to Unix support Header bridge.

> open .

[Stack Overflow Link](https://stackoverflow.com/questions/42516777/is-docker-running-within-wsl-or-connecting-back-to-windows/55075969#55075969)

## ZSH on Windows

How to install 'zsh' in windows 10 WSL subsystem & it also shares proper screenshots along the guide. Very easy to follow - [Link](https://www.maketecheasier.com/install-zsh-and-oh-my-zsh-windows10/)

