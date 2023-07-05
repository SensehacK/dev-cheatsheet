Code Checkout


## SSH

Generating the public - private key pair signature for uploading on Git providers online to directly clone repositories without extra input.
Keeps checking out code limited to specific machines rather than the user.


[SSH Passphrase avoidance](https://superuser.com/questions/988185/how-to-avoid-being-asked-enter-passphrase-for-key-when-im-doing-ssh-operatio)


## Test SSH

You can use these commands to test your ssh configuration in the terminal of your choice.
```bash
ssh -T git@github.com
ssh -T git@github.domain.com
```

## Multiple SSH

In your git config file in directory `~/.ssh` you need to open up the `Config` file in a text editor.
Make sure your subdomains and different enterprise accounts have setup properly to get appropriate ssh key configured.

```text
Host *.HOSTNAME
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/_git_p

Host github.subDomain.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/_git_p

Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/github_no_sub_domain
```