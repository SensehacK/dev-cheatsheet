# Remote

## Git Tokens

Add tokens [here](https://github.com/settings/tokens)

[Link](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line)

1. Click on your Profile Icon (top-right on Github website)
2. Settings
3. Developer settings (bottom-left)
4. Personal access tokens
5. fine-grained tokens
6. "Generate new token"
7. Write a Token name
8. Pick an expiration date from the menu or a custom one
9. Repository access> All repositories
10. Open "Repository permissions" menu
11. Look for the "Contents" row
12. From the menu at right select "Access> Read and Write"
13. "Generate token" (bottom-left)



## Github Gist

Authentication Github Gist using “Github Desktop” didn’t work for me. My main password didn’t work so I created one more Github Token for just “Gist” permission.

And by opening iTerm2 via Github Desktop I was able to push the gist changes by entering my newly generate authorization token.

## Check Remote

Check Git Remote urls on CLI

```sh
git remote -v
```

## Changing Remote

Changing remote origin git urls.

```sh
# remove origin
git remote remove origin
```

```config
`https://github.com/SensehacK/repo\_name`
`repo_full_url` = https://SensehacK:github_pat_token_@github.com/SensehacK/dev-cheatsheet
```
Add the newly updated remote origin with personal access token (PAT)
```sh
git remote add origin `repo_full_url`
```

```sh
git remote set-url origin repo_full_url

git push --set-upstream origin main

git remote add origin 
```

[github remote url](https://help.github.com/en/github/using-git/changing-a-remotes-url)
