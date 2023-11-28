
## PIP


```sh
pip install packageName
## Example
pip install Django
```
[Python Package Index](https://pypi.org/) 

## Poetry

Installing Poetry macOS 
python 3 and sym link issues
```error
dyld[66537]: Library not loaded: @loader_path/../../../../Python.framework/Versions/3.11/Python
```

### Solution
In a conclusion:  
1, download the install script, curl -sSL [https://install.python-poetry.org](https://install.python-poetry.org) > poetry_install.py  
2, change the symlink to True on line 317  
3, python3 poetry_install.py

that's it

https://github.com/python-poetry/install.python-poetry.org/issues/24



### ohmysh zsh issues

command not found for poetry - zsh

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