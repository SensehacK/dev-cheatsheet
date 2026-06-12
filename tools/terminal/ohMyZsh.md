
## Errors


### homebrew opt x86

```error
Last login: Wed Jun 25 12:28:54 on ttys005
/Users/kss7/.zprofile:1: no such file or directory: /opt/homebrew/bin/brew
 ~/git/cloud/-android/-apple 
❯
```
 
Was able to solve this by removing the `opt/homebrew` eval in `.zprofile` instead of `.zshrc` 

And appending that with following config. It seems the classic homebrew installation on x86 (rosetta 2) vs arm (M) architecture issues.

```sh
# slack overflow error no such file 
# https://apple.stackexchange.com/questions/419442/terminal-opens-with-zprofile6-no-such-file-or-directory-opt-homebrew-bin-b
eval "$(/usr/local/bin/brew shellenv)"


# Old context 
# eval $(/opt/homebrew/bin/brew shellenv)
```




### ohmysh or Zsh issues coming from bash environment

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

## Plugins

[Xcode](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/xcode)