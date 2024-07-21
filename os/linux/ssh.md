

## Command

```sh
ssh username@10.0.0.11 -vvvvA
```

Providing `-vvvvA` will give you debug logs for ssh connection.


## Generate Key

[Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)


## Adding Key

Adding a new SSH key to your Git Cloud hosted service
- [Github](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) 


## Auto SSH

It is like a daemon to monitor the service / like a watchdog to restart the service if it crashes or stops abruptly.
[autossh restart](https://www.harding.motd.ca/autossh/)

 [Stack Exchange | How to reliably keep an SSH tunnel open?](https://superuser.com/questions/37738/how-to-reliably-keep-an-ssh-tunnel-open) 


## Copy Files SCP


```sh
scp nomachine_8.11.3_5.dmg username@10.523.325.212:/Users/username/directoryName
```

[how-to-use-scp-to-transfer-files-in-the-macos-terminal](https://appleinsider.com/inside/macos/tips/how-to-use-scp-to-transfer-files-in-the-macos-terminal)



## netrc

Auto Login | netrc
The .netrc file contains login and initialization information used by the auto-login process. It generally resides in the user’s home directory, but a location outside of the home directory can be set using the environment variable `NETRC`. Both locations are overridden by the command line option -N. The selected file must be a regular file, or access will be denied.

[gnu source](https://www.gnu.org/software/inetutils/manual/html_node/The-_002enetrc-file.html)

[curl netrc information](https://everything.curl.dev/usingcurl/netrc.html)

For us using the netrc file does the trick. But note that besides:

```swift
machine github.com
  login <username>
  password <personal access token>
```

You also need to add this if your Package.swift points to binaries stored in GitHub package registry:

```swift
machine maven.pkg.github.com
  login <username>
  password <personal access token>
```

Took me quite a while to figure this out, but sub domains are not included in the machine definitions, so specify them individually.

[swift forums thread source | resolving private packages through HTTPS with xcodebuild](https://forums.swift.org/t/support-for-resolving-private-packages-through-https-with-xcodebuild/48581)


## Errors

`kex_exchange_identification: Connection closed by remote host`
