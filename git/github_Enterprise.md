
# Github Enterprise


## Mind Map

[github](github.md)

[github_enterprise](github_enterprise.md)

[github_actions](github_actions.md)


## Errors

Could not read username - terminal prompts disabled.
I'm assuming this is because my ssh username or account hasn't been added to the github enterprise SSO known lists to clone repo. 
OR
something inherently wrong with my ssh setup.

```text
A shell task (/usr/bin/env git clone --bare --quiet https://github..com/aae-ios/FastCoderFramework.git /Users/ksave/Library/Caches/org.carthage.CarthageKit/dependencies/FastCoderFramework) failed with exit code 128:
fatal: could not read Username for 'https://github.website.com': terminal prompts disabled
```



Git replace of https to ssh URL in local config

```bash
git config --local url.ssh://git@github.company.com/.insteadOf https://github.company.com/
```

You can find these changes in `.git` folder with `config` file where you can remove these things.


### Error: Resource protected by organization SAML enforcement.

```sh
Error: Resource protected by organization SAML enforcement. You must grant your Personal Access token access to an organization within this enterprise.
```
Probably have to give the token access to those specific organizations.

## Workflow


[github actions variables](docs.github.com/en/actions/learn-github-actions/variables)

[events triggering](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows) 

[SO | run when pull requests have a specific label](https://stackoverflow.com/questions/62325286/run-github-actions-when-pull-requests-have-a-specific-label)

[github project automation workflow](https://github.com/alex-page/github-project-automation-plus)


## Tokens

Creating access tokens for your account to access repositories or github related stuff can be [created here in github settings](https://github.com/settings/tokens/new?)

Creating secrets like environment variables can be [read here from github official docs](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions#creating-encrypted-secrets-for-a-repository)

## Debugging

### Skipped the job

[Github thread](https://github.com/orgs/community/discussions/36007)

### Debug logs

Location can be found in `actions-runner/_diag/` in your main home directory of your custom github runner.
[Enable debug logging on github actions workflows](https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/enabling-debug-logging)


## Extension

Had some issues with Github Pull Requests, Projects and issues popping up on my VS code left side bar. But after I signed out my own personal account it automatically asked me sign again with my work account github enterprise cloud. 
Voila it works splendid just like VS code on web.
Glorious
If you're reviewing a PR you can just press `.` to simulate like a terminal bash/zsh command of `code .` in the current path to open up the PR or project branch in VS code. Pretty nice for reviewing spec or web PRs when there's no requirement of specific language intellisense for swift | xcode or other dependency.
