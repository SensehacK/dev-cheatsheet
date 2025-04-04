# Shell

## Terminal Key Tags

Tilde\(~\) is used to denote a user's home directory whereas slash\(/\) is used for separators for filesystem objects in both absolute paths and relative paths. Also it is used for to represent the root directory. On a side note: ~/ is used to denote beginning of a path to a file or directory below the user's home directory.

New Variables Key Tags

In short, if the screen shows a dollar sign \($\) or hash \(\#\) on the left of the blinking cursor, you are in the command line environment.

$, \#, % symbols indicate the user account type you are logged in to.

Dollar sign \($\) means you are a normal user. hash \(\#\) means you are the system administrator \(root\). In the C shell, the prompt ends with percentage sign \(%\). There are differences on prompts in different Unix or GNU/Linux distributions because of their default settings. For example, the prompt of Debian/Ubuntu is guest@linux:~$, the one of Fedora/CentOS/RedHat is \[guest@linux ~\]and the one of SuSE Linux/OpenSUSE is guest@linux:~&gt;. In general, the prompt usually show the login user name, machine hostname and current working directory and ended with a dollar \($\), percentage \(%\) or hash \(\#\) sign.

guest@linux:~guest - username: the user account you are logged in to. linux - machine hostname: the machine you are operating. ~ - current working directory: the directory you are in. Tilde \(~\) means home directory, i.e. the default directory when first logging in. Source: wiki.debian.org.hk/w/Basic\_Command\_Line

## Access permissions

Changes all the ownership for folders

```sh
sudo chown -R \`whoami'
```

Specific folder ownership // User: defines just user // $USER:$USER has user group also.

```sh
sudo chown -R user: ~/.virtualenvs sudo chown $USER:$USER /usr/local/bin/youtube-dl
```

## Terminal commands

Will actually reset the terminal, which wont be shown after scrolling with command ‘clear’

```sh
reset 
clear
```

Deleting History

```sh
history -c 
history -a
```

Doing a:

```sh
history -c; 
history -w
```

Will clear history in memory and write that to the HISTFILE file. That will clear both memory and file history.

If it is required that nothing else of the present session would be written to the history, then, unset HISTFILE will prevent any such logging.

## Directory

The command ls -a list all files, including hidden ones, but I need just to list hidden files. Will only list hidden files .

```sh
ls -ld .?\*
```

change directory

```sh
cd directory\_name
```

List directory contents

```sh
ls
```

Current Directory

```sh
pwd
```

Opening current folder

```sh
open .
```

go back parent directory

```sh
cd ..
```

Favorite directories ~ User Directory & / Root directory

```sh
cd 
cd /
```

Visual studio open

```sh
code .
```

Mac Text to Speech command

```sh
say "Hello Kautilya"
```

## NPM Electron

Electron Project GUI To use the application:

1. Clone the project
2. Run npm install
3. Run npm start

## Bash Script

Always filter these keywords with

```sh
\&
```

I have wished for a "complete list". I used to have a filter program compiled that would escape every "special character" that I could think of.

A good start: ! ? % \# & \* \( \) blank tab \| ' ; " &lt; &gt;  ~ \` \[ \] { }

[gnu | bash - escape char](https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html#Escape-Character)

## Deletion

Source : [https://askubuntu.com/questions/60228/how-to-remove-all-files-from-a-directory/60229](https://askubuntu.com/questions/60228/how-to-remove-all-files-from-a-directory/60229)

To remove the folder with all its contents\(including all interior folders\):

```sh
rm -rf /path/to/directory
```

To remove all the contents of the folder\(including all interior folders\) but not the folder itself:

```sh
rm -rf /path/to/directory/\*
```

or

```sh
rm -rf /path/to/directory/{_,._}
```

if you want to make sure that hidden files/directories are also removed.

To remove all the "files" from inside a folder\(not removing interior folders\):

```sh
rm -f /path/to/directory/{_,._}
```

Warning: if you have spaces in your path, make sure to always use quotes.

```sh
rm -rf /path/to the/directory/\*
```

is equivalent to 2 separate rm -rf calls:

```sh
rm -rf /path/to rm -rf the/directory/\*
```

To avoid this issue, you can use 'single-quotes'\(does not expand shell variables\) or "double-quotes"\(expands shell variables\):

```sh
rm -rf "/path/to the/directory/"\*
```

Where:

rm - stands for "remove" -f - stands for "force" which is helpful when you don't want to be asked/prompted if you want to remove an archive, for example. -r - stands for "recursive" which means that you want to go recursively down every folder and remove everything.

## Secure Delete

Use rm with flag -P for overwriting the file so that it won't be recovered easily. Still it doesn't guarantee files being securely deleted.

```sh
rm -P "filename.fileExtension"
```

## Previous Commands

We can access previous commands by using '!' parameter and also specify which parameter we want to swap for faster commands cycling.

Command 1:

```sh
mkdir test_git
```

This will utilize the first parameter of previous command.

```sh
cd !:1 # cd test_git
```

```sh

!:0 = the name of command executed.

!:1 = the first parameter of the previous command

!:* = all of the parameters of the previous command

!:-1 = the final parameter of the previous command

!! = the previous command line

```

[SO](https://stackoverflow.com/a/9502698)

## Reload Terminal

Loading the terminal with latest settings without logging out. 

You can enter the long form command:

```sh
source ~/.bashrc
```

or you can use the shorter version of the command:

```sh
. ~/.bashrc
```

[SO](https://stackoverflow.com/questions/2518127/how-to-reload-bashrc-settings-without-logging-out-and-back-in-again)

### ZSH

You can enter the long form command:

```bash
source ~/.zshrc
```

or you can use the shorter version of the command:

```bash
. ~/.zshrc
```

[SO | how-to-load-bash-profile-when-entering-bash-from-within-zsh](https://stackoverflow.com/questions/23233603/how-to-load-bash-profile-when-entering-bash-from-within-zsh)



## Arch

```sh
arch
```


## Errors


### zsh issues


ohmysh or Zsh issues coming from bash environment

`command not found`


for poetry - zsh
I did a fresh install with `zsh` and `prezto` installed. Below is the same case with me. Poetry installs to `.local`  even though I haven't had any `.local`  directory before...


```shell
# User specific environment
if ! [[ "$PATH" =~ "$HOME/.local/bin:$HOME/bin:" ]]
then
    PATH="$HOME/.local/bin:$HOME/bin:$PATH"
fi
export PATH
```

Added this to `.zhsrc` 
Freaking hate command line environment setups just to run a small script


[SO | Post homebrew permissions](https://stackoverflow.com/questions/16432071/how-to-fix-homebrew-permissions/46844441#46844441)

Basically it could stem from bad install script and using `sudo` where it wasn't needed which leads to all this permission errors.
[Github | homebrew permission denied thread](https://github.com/Homebrew/legacy-homebrew/issues/19670)



New command for users on macOS High Sierra as it is not possible to `chown` on `/usr/local`:

`bash/zsh`:

```sh
sudo chown -R $(whoami) $(brew --prefix)/*
```

`fish`:

```sh
sudo chown -R (whoami) (brew --prefix)/*
```