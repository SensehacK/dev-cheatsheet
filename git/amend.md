# amend
**


## Amend author

If you want to change the author details of the commit message, you can do it using flag `--amend`

```sh
git commit --amend --author="Kautilya <kautilya@email.com>"
git commit --amend --author="Kautilya <kautilya.save@product_name.com>"
```


[Tower author change](https://www.git-tower.com/learn/git/faq/change-author-name-email/)

[SO | change commit for one commit ](https://stackoverflow.com/questions/3042437/how-to-change-the-commit-author-for-one-specific-commit)

Error if you have an index lock error refer to [errors](git/errors.md)

## Change Timestamp


This only works for the last commit in the git history tree.

```bash
git commit --amend --date=now

git commit --amend --no-edit --date=now

git commit --amend --no-edit --date "2001-09-11T12:14:00-00:00"
```

[SO change-the-timestamp-of-an-old-commit](https://stackoverflow.com/questions/454734/how-can-one-change-the-timestamp-of-an-old-commit-in-git)
[Git Commit Date with alias](https://dev.to/itsmohamedyahia/how-to-change-a-git-commit-date-for-beginners-40ge)

Going with Environment variable way to trick git into committing the date time on its amend operation
```sh
GIT_COMMITTER_DATE=<date> git commit --amend --no-edit --date <date>
```
[rebasing and amending commit date](https://sabe.io/blog/change-date-git-commit)

Or combined both

```sh
LC_ALL=C GIT_COMMITTER_DATE="$(date)" git commit --amend --no-edit --date "$(date)"
```

## Empty Commit 

Sometimes we want to not commit anything and just need some change set in order to trigger a build on CI or Github Actions.

```sh
git commit --allow-empty -m "bump for CI"
git push 
```


## Specific commit amend 

`~` is important 
Please note the tilde `~` at the end of the command, because you need to reapply commits on top of the previous commit of `cec643cd` (i.e. `cec643cd~`).

```sh
git rebase --interactive cec643cd~
```

Then use `i` for insert, esc for `:`, `:w` for write, `:q` for quit.

[vim modes](modes.md)

so now you're on `cec643cd` commit & you can edit few things

```sh
git commit --amend
```

Check author date, commit date from logs.
```sh
git log --format=fuller
```
squash the commits and then you can remove that commit.
Switch to soft when you want to delete the head commit but also keep the untracked files.

remove last commit and put it in unchanged stage changes.
you can use `--hard` if you don't want those changes in changeset.

```sh
git reset --soft HEAD~
```


[SO | modify specific commit](https://stackoverflow.com/questions/1186535/how-do-i-modify-a-specific-commit)

## Cherry Pick

Cherry picking git commits

```sh
git cherry-pick `git_hash`
git cherry-pick 03d6929
```

Sometimes if the commit is present already with its changes it will present this message.

```sh
nothing to commit, working tree clean
The previous cherry-pick is now empty, possibly due to conflict resolution.
If you wish to commit it anyway, use:

git commit --allow-empty

Otherwise, please use 'git cherry-pick --skip'
```




## References

[Git cherry pick Man page](https://git-scm.com/docs/git-cherry-pick)

[Github Desktop cherry Pick guide](https://docs.github.com/en/desktop/managing-commits/cherry-picking-a-commit-in-github-desktop)

[Atlassian | cherry pick](https://www.atlassian.com/git/tutorials/cherry-pick)