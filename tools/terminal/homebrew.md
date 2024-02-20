
# HomeBrew

## Intro


## Commands

Gives you the home brew version installed on your machine.

```sh
brew -v
```

## Packages

### Tree package

Listing all of the folder and files in the present directory.

Great for just sharing project structures online.

```sh
tree -L 3
tree —help
```
where -L level Descend only level directories deep with integer parameter. tree —help For getting the list of commands.


### path update

[SO zsh command not found brew](https://stackoverflow.com/questions/36657321/after-installing-homebrew-i-get-zsh-command-not-found-brew)


## CLI JSON Processor

```sh
brew install jq
```

[Github | jq](https://github.com/jqlang/jq)
[Online tool to parse logic on JSON data](https://jqplay.org/)

## Rosetta ARM

Conflicting package arm architecture issues when installing a package. You can run the same command with a prefix of arch type.

```sh
arch -arm64 brew install package_name
```

[SO error cannot install under rosetta 2](https://stackoverflow.com/questions/74310340/error-cannot-install-under-rosetta-2-in-arm-default-prefix-opt-homebrew)
