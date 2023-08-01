# Checkout



## Description

Turns out I couldn't use & in the branch name of a git checkout for pulling information.
That's what I was getting an error about it when I tried to use our internal git  support tool which checks out branches on different layers.


```sh
bug/TV-00000-Offline-&-Sync-crash --fallback release/asfka 
[1] 26872
zsh: command not found: -Sync-crash
```



## Fetch Error

```sh
fatal: bad object refs/heads/master (DESKTOP-0PQ7OJL's conflicted copy 2023-04-11) error: https://github.com/SensehacK/terminal_cheatsheet.git did not send all necessary objects
```

This is happening because I used dropbox as the background service directory to quickly sync everything as much as possible and also push those changes to `github` repo `dev-cheatsheet`.


## Terminal Prompt Disabled

Just clone the repository on a CLI. When running scripts on CI server the terminal prompts are disabled by default.


```sh
A shell task (/usr/bin/env git fetch --prune --quiet [https://github.com/-ios/OHHTTPStubs.git](https://github.com/-ios/OHHTTPStubs.git) refs/tags/*:refs/tags/* +refs/heads/*:refs/heads/* (launched in /Users/jenkins/Library/Caches/org.carthage.CarthageKit/dependencies/OHHTTPStubs)) failed with exit code 128:
fatal: could not read Username for '[https://github.com](https://github.com)': terminal prompts disabled
```