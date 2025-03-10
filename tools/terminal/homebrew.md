
# HomeBrew

## Intro


## Commands

Gives you the home brew version installed on your machine.

```sh
brew -v
```

Home brew configuration dump.

```sh
brew config
```

Gives you the installed location of your homebrew. Helpful to determine whether its x86 or ARM arch.

```sh
which brew
```

### Update Package

```sh
brew upgrade package_name
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

### JQ examples

```sh
# Convert to CSV
curl -s https://api.discogs.com/users/cesarista/collection/folders/0/releases --user-agent "FooBarApp/3.0"| jq '.releases[].basic_information' | jq -r '"\(.id),\(.year),\(.title),\(.artists[0].name),\(.formats[0].name)"'

# Extract / simplify JSON 
curl -s https://api.discogs.com/users/cesarista/collection/folders/0/releases --user-agent "FooBarApp/3.0"| jq '.releases[].basic_information' | jq '. | {id: .id, year: .year, title: .title, artist: .artists[0].name, format: .formats[0].name, label: .labels[0].name}'

# Show first 50 John Lennon releases in Discogs
curl -s https://api.discogs.com/artists/46481/releases | jq '.releases[]' | jq -r '"\(.id),\(.year),\(.title)"'
```

[Github source](https://gist.github.com/CesarCapillas/457f6b7cba9bfa65e36421d4f3e738de)


## Rosetta ARM

Conflicting package arm architecture issues when installing a package. You can run the same command with a prefix of arch type.

```sh
arch -arm64 brew install package_name
```

```log
Cask project_name depends on hardware architecture being one of [{:type=>:arm, :bits=>64}], but you are running {:type=>:intel, :bits=>64}.
```

[SO error cannot install under rosetta 2](https://stackoverflow.com/questions/74310340/error-cannot-install-under-rosetta-2-in-arm-default-prefix-opt-homebrew)



## Delete | uninstall


```sh
brew uninstall <package_name>
```



## Support both x86 | ARM

[Source Git Gist](https://gist.github.com/progrium/b286cd8c82ce0825b2eb3b0b3a0720a0)

### Key Points
* In general, binaries built just for x86 architecture will automatically be run in x86 mode
* You can force apps in Rosetta 2 / x86 mode by right-clicking app, click Get Info, check "Open using Rosetta"
* You can force command-line apps by prefixing with `arch -x86_64`, for example `arch -x86_64 go`
* Running a shell in this mode means you don't have to prefix commands: `arch -x86_64 zsh` then `go` or whatever
* Don't just immediately install Homebrew as usual. It should most likely be installed in x86 mode.


### Homebrew
Not all toolchains and libraries properly support M1 arm64 chips just yet. Although 
automatic x86 mode works pretty well, more complex build toolchains use multiple programs that should all be
building for the same architecture. Since we often use Homebrew to install these toolchains, it might be
best to install the x86 "version" of Homebrew, otherwise it will install arm64 versions of things.

*Just be sure to run the Homebrew install command in an x86 shell*

```sh
$ arch -x86_64 zsh
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
From here, as long as you're in this x86 zsh shell, you can use Homebrew as usual to install x86 packages:

```sh
brew install go
```

You'll know it's the right version because it will install into `/usr/local` instead of the usual `/opt`. 
This also means you can install both versions of Homebrew, and arm64 packages will live under the `/opt` instance.
However, unless necessary I wouldn't recommend it because I can imagine accidentally using the wrong version 
pretty easily. If you only have one version, you can install packages without entering x86 zsh, just prefix with `arch -x86_64`:

```sh
arch -x86_64 brew install go
```

If you install both versions, you'll also need to specify the full path to the `brew` binary as one will live under `/opt`
and one will live under `/usr/local`.

### Tips 

#### Terminal Trick
If you duplicate your terminal application (Terminal, iTerm, etc) and set the new one to "Open using Rosetta", then you have a quick way into a terminal and shell in either mode. Thanks for the tip [@tmc](https://github.com/tmc)

#### Golang Cross Compiling
Although used in the examples, if you just want to work with Go, you should be able to just use `GOARCH` to produce an x86_64 binary using an arm64 go binary. This probably won't work so smoothly if you're using CGO.

#### Checking Architecture
Remember you can always use the `file` command on a binary to see what architecture its built for.


## Architecture

checks the hardware or terminal which is running for it.

```sh
uname -m
```

prints values such as `x86_64`, `i686`, `arm`, or `aarch64`.



## Errors


### Failed to link all completions

```
Permission denied @ rb_file_s_symlink - (../../../Homebrew/completions/zsh/_brew, /usr/local/share/zsh/site-functions/_brew)

Failed during: /usr/local/bin/brew update --force --quiet...
```

Solution - permission error
```
Yes, it entirely explains the "permission denied" error you got. `sudo chown -R $(whoami) /usr/local/share/zsh/site-functions` should fix that, then run the Homebrew installer again to ensure everything is installed correctly.
```

Makes sure your firewall isn't blocking certain things on it and have your VPN turned off maybe for easier debugging.

[Github | thread](https://github.com/orgs/Homebrew/discussions/3227)

