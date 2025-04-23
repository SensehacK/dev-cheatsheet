# Git Errors

## CLI

### There was a problem with the editor git

I actually get this error quite often when I was using vim for `git commit`. Whenever finish typing the commit message and `:wq`, any typo will kill the commit message and returns this error `error: There was a problem with the editor 'vi'.` which is really frustrating.

Fortunately, here's the solution:

```sh
git config --global core.editor $(which vim)
```

## Desktop

### Commit failed - exit code 1

Users have run into this error due to having nested .git directories. [Issue Link](https://github.com/desktop/desktop/issues/4432)


### getaddrinfo() thread failed

```sh
fatal: unable to access 'url.git/': getaddrinfo() thread failed to start
```

This could be because the machine which is cloning the repository or trying git fetch is on different vpn. And Github preemptively disables letting someone clone if its from different geo codes/ zone.
Kind of a security measure. 
So disable your whole OS tunnel vpn and fetch it again.
Also similar [Stack Overflow post confirms the VPN usage conflicting git fetch errors](https://stackoverflow.com/a/37573183)


## Cloud

### remote: Write access to repository not granted.

fatal: unable to access 'https://github.com/': The requested URL returned error: 403
Make sure if you select `fine grained tokens` add `Contents` permission as `Read and Write` option checked in order to properly push changes to the repo.


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

Or your personal Access token is expired so you're getting this error according to [Github issue thread](https://github.com/actions/checkout/issues/664)

If you use `xcodebuild -scmProvider xcode`, HTTPS can be used, but you would typically log in via Xcode preferences to your SCM service account.

### getaddrInfo thread


```sh
fatal: unable to access 'https://github.com/<github-username>/<repository-name>.git/': getaddrinfo() thread failed to start
```

Turning off VPN or antivirus/firewall to add the github.com domain to allow list helped me get past this error.
[SO | fatal-unable-to-access-link-getaddrinfo-thread-failed-to-start](https://stackoverflow.com/questions/59911649/fatal-unable-to-access-link-getaddrinfo-thread-failed-to-start)


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



### Connection reset by peer

I don't know why it failed on this but after re-running the CI it worked fine again.

```sh
fatal: unable to access 'https://github.com/PromiseKit/Alamofire/': Recv failure: Connection reset by peer
```



## remote_repository_not_found


```
remote: Repository not found.
fatal: repository 'https://github.com/MyRepo/project.git/' not found
```

[SO | Git - remote: Repository not found](https://stackoverflow.com/questions/37813568/git-remote-repository-not-found)

the stack overflow post didn't help, I even tried to log out from Github desktop to get the new token. Deleted the old keychain access login items for `github.com` & also for some reason my `ssh` token identity had been revoked for SSO access for my specific organization. 1 out of 5 were only allowed & I always need 3 of them.
So I created a new branch and tried to push & now it works. 
In the whole scenario I did force restart my Github Desktop application so maybe the SSO revoke / access thing got re-triggered ? or old cache was discarded. Anyway I was able to push it.


## exit code 74

```sh
Build Failed
	Task failed with exit code 74
```

For me I just opened the `.xcode` proj in gui and selected the rosetta simulator since the xcode output logs generated by carthage wasn't showing anything else.
I build it via GUI and then again ran the command for carthage and this time it worked properly.
Also I deleted my keychain entries for github cloning and closed xcode before as well. Don't know if that's related or not but just throwing it out there the steps I took to make it work.


## Cannot lock head

```sh
Git cannot lock ref 'HEAD': unable to resolve reference HEAD
```


[SO | unable to lock HEAD](https://stackoverflow.com/questions/39057962/git-cannot-lock-ref-head-unable-to-resolve-reference-head)


## Unable to create index.lock

```log
Git - fatal: Unable to create '/path/my_project/.git/index.lock': File exists
```


Just remove the temporary `.lock` file from the system.

```sh
rm -f ./.git/index.lock
```