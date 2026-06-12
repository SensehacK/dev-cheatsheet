
# Git Info

Various Git commands handy cheatsheet.




These are default git commands normally used in a project.
I usually use "Github Desktop" due to GUI and how easy it is to download my repositories from github.com & it's free.

My all time favorite is "Tower" git client and favorite enterprise git SaaS is "Gitlab" for personal use "github".

## Syntax

Fast one liners for easy reference.

### Current Status

Gives you the status of the current repository

```sh
git status 
```

### Git version

Gives you the git tools installed on your machine.

```sh
git version
```


### Fetch

```sh
git fetch origin_url
```

```sh
git pull 
```

### Commit

```sh
git add -A
```

```sh
git commit -m 'Commit message' 
```

### Push

```sh
git push
```

### Branching

```sh
git checkout branch_name
```


## Get Hash

This command directly outputs the full SHA-1 hash of the commit pointed to by HEAD.
```sh
git rev-parse HEAD
```


## History

Displays the git logs overall
```sh
git log
```

This command uses `git log` to display commit history, but with specific options: 

- `-n 1`: Limits the output to only the most recent commit.
- `--pretty=format:%H`: Formats the output to show only the full commit hash (`%H`).
```sh
git log -n 1 --pretty=format:%H
```

### Hash lookup

Get full commit hash from short hash
`git rev-parse` will give you what you want.

```sh
git rev-parse 03d6929
```
