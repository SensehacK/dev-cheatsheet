# Terminal commands for Mac

## Terminal Key Tags

Tilde(~) is used to denote a user's home directory whereas slash(/) is used for separators for filesystem objects in both absolute paths and relative paths. Also it is used for to represent the root directory.
On a side note:
~/ is used to denote beginning of a path to a file or directory below the user's home directory.

New Variables Key Tags

In short, if the screen shows a dollar sign (\$) or hash (#) on the left of the blinking cursor, you are in the command line environment.

\$, #, % symbols indicate the user account type you are logged in to.

Dollar sign (\$) means you are a normal user.
hash (#) means you are the system administrator (root).
In the C shell, the prompt ends with percentage sign (%).
There are differences on prompts in different Unix or GNU/Linux distributions because of their default settings. For example, the prompt of Debian/Ubuntu is guest@linux:~$, the one of Fedora/CentOS/RedHat is [guest@linux ~]$ and the one of SuSE Linux/OpenSUSE is guest@linux:~>. In general, the prompt usually show the login user name, machine hostname and current working directory and ended with a dollar (\$), percentage (%) or hash (#) sign.

guest@linux:~\$
guest - username: the user account you are logged in to.
linux - machine hostname: the machine you are operating.
~ - current working directory: the directory you are in. Tilde (~) means home directory, i.e. the default directory when first logging in.
Source: wiki.debian.org.hk/w/Basic_Command_Line

## Access permissions

Changes all the ownership for folders

> \$ sudo chown -R `whoami'

Specific folder ownership
// User: defines just user
// $USER:$USER has user group also.

> sudo chown -R user: ~/.virtualenvs
> sudo chown $USER:$USER /usr/local/bin/youtube-dl


## Terminal commands

Will actually reset the terminal, which wont be shown after scrolling with command ‘clear’

> \$ reset
> \$ clear

Deleting History

> \$ history -c
> \$ history -a

Doing a:

> \$ history -c; history -w

Will clear history in memory and write that to the HISTFILE file.
That will clear both memory and file history.

If it is required that nothing else of the present session would be written to the history, then, unset HISTFILE will prevent any such logging.

## Directory

The command ls -a list all files, including hidden ones, but I need just to list hidden files.
Will only list hidden files .

> \$ ls -ld .?\*

change directory

> \$ cd directory_name

List directory contents

> \$ ls

Current Directory

> \$ pwd

Opening current folder

> \$ open .

go back parent directory

> \$ cd ..

Favorite directories
~ User Directory & / Root directory

> \$ cd ~
> \$ cd /

Visual studio open

> \$ code .

Mac Text to Speech command

> say "Hello Kautilya"

## NPM Electron

Electron Project GUI
To use the application:

1. Clone the project
2. Run npm install
3. Run npm start

## Bash Script

Always filter these keywords with

> \$ \&

I have wished for a "complete list". I used to have a filter program compiled that would escape every "special character" that I could think of.

A good start: ! ? $ % $ # & \* ( ) blank tab | ' ; " < > \ ~ ` [ ] { }
