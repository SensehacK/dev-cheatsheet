
## Install

Install or download python executable from [official website](https://www.python.org/downloads/)

[macOS](https://www.python.org/downloads/macos/)

home brew route

```sh
brew install python
```

SET Path

[path macOS guide](https://mac.install.guide/python/path)

[path](os/mac/path.md)



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
[github thread issue](https://github.com/python-poetry/install.python-poetry.org/issues/24)







## Errors

### error: externally-managed-environment


```log
This environment is externally managed
╰─> To install Python packages system-wide, try brew install
    xyz, where xyz is the package you are trying to
    install.

    If you wish to install a Python library that isn't in Homebrew,
    use a virtual environment:

    python3 -m venv path/to/venv
    source path/to/venv/bin/activate
    python3 -m pip install xyz

    If you wish to install a Python application that isn't in Homebrew,
    it may be easiest to use 'pipx install xyz', which will manage a
    virtual environment for you. You can install pipx with

    brew install pipx

    You may restore the old behavior of pip by passing
    the '--break-system-packages' flag to pip, or by adding
    'break-system-packages = true' to your pip.conf file. The latter
    will permanently disable this error.

    If you disable this error, we STRONGLY recommend that you additionally
    pass the '--user' flag to pip, or set 'user = true' in your pip.conf
    file. Failure to do this can result in a broken Homebrew installation.

    Read more about this behavior here: <https://peps.python.org/pep-0668/>
```

