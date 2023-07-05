

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
git config --local url.ssh://git@github.comcast.com/.insteadOf https://github.comcast.com/
```

You can find these changes in `.git` folder with `config` file where you can remove these things.