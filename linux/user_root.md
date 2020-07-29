# I am Root

## Basics

There is normal user and then there is super user \(root\) which has administrative access over the O.S ecosystem.  
Normal circumstances don't require a person to be logged in as admin/root so by default most of the linux distros will have normal user profile.

Still sometimes you need to gain root user permission in order to perform elevated commands which modifies the system in some way in the background.

We can reach that elevated user permission by two methods

* Temporary root user
* Root shell user

Usually it is advisable to use temporary root user as it prevents from having too much power at default shell.

### Temporary root user

If you're familiar with linux ecosystem or any of the unix subsystem which houses bash or zsh. You may have ran into using commands like

> sudo apt-get install some\_package\_name

That `sudo` command is what makes you a temporary root access from normal user for executing that specific command for the time being. After you hit enter you need to enter the password for the root user.

### Root Shell user

Just type in shell and enter

> su -

Enter the root credentials and if you don't have any just refer to this [link](https://vitux.com/how-to-become-root-user-in-ubuntu-command-line-using-su-and-sudo/) which explains how to reset your user credentials of any user.

You can verify which user you're currently logged in via the command

> whoami

which will return the user logged in.

Linux WSL on Windows is great so far.

As long as I have linux subsystem running on windows natively, I won't be missing macOS for development purposes aside from native iOS app development. I do miss the apps ecosystem like "Things", "Fantastical", "iTerm2" and "Spark".

Also I'm loving the Windows Terminal which I'll make the default shell of Linux Ubuntu. [Link](https://superuser.com/questions/1456511/is-there-a-way-to-change-the-default-shell-in-windows-terminal)

