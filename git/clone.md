# Clone | Checkout



## Description

We are at this step of Software Development hell. Git checkout configurations. Some say the hardest thing in development is naming the variables meaningful and configuring your workstation with appropriate fine grain authorization.
If the project has been configured appropriately by a senior engineer or a security team, it should be as a fool proof as possible to not have any destruction by anyone who knows nothing about code versioning.


## Getting Started

First task would be setting up your workstation with appropriate credentials using `https` or `ssh` based approach in order for you to clone the code.

I recommend `ssh` approach and you can refer to my [guide here](../os/linux/ssh.md#Generate%20Key)
After that you can add that key to your [git cloud provider here](../os/linux/ssh.md#Adding%20Key) 

## Syntax

```sh
git clone repoURL/repoProject.git
```

[git scm book cloning](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository)
## Error
### Fetch Error

```sh
fatal: bad object refs/heads/master (DESKTOP-0PQ7OJL's conflicted copy 2023-04-11) error: https://github.com/SensehacK/terminal_cheatsheet.git did not send all necessary objects
```

This is happening because I used dropbox as the background service directory to quickly sync everything as much as possible and also push those changes to `github` repo `dev-cheatsheet`.



### Branch checkout pull Issues

Turns out I couldn't use & in the branch name of a git checkout for pulling information.
That's what I was getting an error about it when I tried to use our internal git  support tool which checks out branches on different layers.

```sh
bug/TV-00000-Offline-&-Sync-crash --fallback release/asfka 
[1] 26872
zsh: command not found: -Sync-crash
```
### Terminal Prompt Disabled

Just clone the repository on a CLI. When running scripts on CI server the terminal prompts are disabled by default.


```sh
A shell task (/usr/bin/env git fetch --prune --quiet [https://github.com/-ios/OHHTTPStubs.git](https://github.com/-ios/OHHTTPStubs.git) refs/tags/*:refs/tags/* +refs/heads/*:refs/heads/* (launched in /Users/jenkins/Library/Caches/org.carthage.CarthageKit/dependencies/OHHTTPStubs)) failed with exit code 128:
fatal: could not read Username for '[https://github.com](https://github.com)': terminal prompts disabled
```

Or your personal Access token is expired so you're getting this error according to Github issue thread.
https://github.com/actions/checkout/issues/664


### getaddrInfo thread


```bash
fatal: unable to access 'https://github.com/<github-username>/<repository-name>.git/': getaddrinfo() thread failed to start
```

Turning off VPN or antivirus/firewall to add the github.com domain to allow list helped me get past this error.
https://stackoverflow.com/questions/59911649/fatal-unable-to-access-link-getaddrinfo-thread-failed-to-start

### Host key verification failed

Error when cloning the repository.

```sh
Failed to connect to repository : Command "git Is-remote -h -- git@github.com:company_name/repo_name.git

HEAD" returned status code 128:

stdout:

@ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! @

IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!

Someone could be eavesdropping on you right now (man-in-the-middle attack)!

it is also possible that a host key has just been changed.

The fingerprint for the RSA key sent by the remote host is

SHA256:asfgagaw.

Please contact your system administrator.

Add correct host key in /Users/jenkins/.ssh/known_hosts to get rid of this message.

Offending RSA key in /Users/jenkins/.ssh/known_hosts:9

Host key for [ssh.github.com]:443 has changed and you have requested strict checking.

Host key verification failed.

fatal: Could not read from remote repository.

Please make sure you have the correct access rights

and the repository exists.
```

This happens when you have the same credentials setup on your machine which has `old_remote_git` and `new_remote_git` endpoints access. But since the git config has been setup with `strict checking` which is good for enterprise IMO. It makes a warning and early exit of making sure there's some user intervention to avoid man in middle attack (eavesdropping) of some kind when cloning rogue repository without making sure the public / private RSA keys have been authenticated with the known hosts.

This can happen when the remote url has been migrated to a new instance or change in remote URL endpoints. The hash checksum (md5/sha1) changes which makes the cloning fail because the host identification in general has changed. You can check the `/user/.ssh/known_host` config file and update the new endpoint's host key in order to appropriately add this endpoint in allowlist/whitelist `known_host` list.


```sh
ssh-keygen -R github.com
```
This also creates a backup of old config of ssh agent.
Which is basically running the command explicitly

```sh
cp ~/.ssh/known_hosts ~/.ssh/known_hosts.bak
```

[ssh-keygen man](https://linux.die.net/man/1/ssh-keygen)

[Stack overflow post](https://serverfault.com/questions/321167/add-correct-host-key-in-known-hosts-multiple-ssh-host-keys-per-hostname)

[Dealing with SSH Host Key Changes](https://cat.pdx.edu/platforms/linux/remote-access/dealing-with-ssh-host-key-changes/)
