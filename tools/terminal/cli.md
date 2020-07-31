# Git

Various Git commands handy cheatsheet.

## Git Stash Commands

Git stash commands comes in handy when needed to pull other branches & the other branch codebase has conflicts with your own branch. This stash utility saves a local copy of your working branch & pulls the new branch & then you can override your local branch with the incoming branch.

```text
> \$ git stash
> \$ git pull --rebase
> \$ git stash apply
```

## Git Branch Commands

If you want to switch to different branch from your current local uncommitted branch you could follow these steps overall.

Step 1 : Local\_Branch\_Name \(Local Changes\) Considering you want to save or forward these changes to your new branch.

Step 2 : Create your newly created branch with base as of updated master or develop.

Step 3 : Run Git stash command to save your workflow.

```text
> \$ git stash
> \$ git checkout branch_name
```

Step 4 : After switching to new branch via Git CLI or Git GUI just run Stash Apply command for overwriting your changes to new branch.

> $ git stash apply

## Git Rebase Commands

## Git Remove Commits

Multiple options if we haven’t pushed the code to origin server.

Option 1 : Undo commit and keep all files staged

> git reset --soft HEAD~;

Option 2 : Undo commit and un-stage all files

```text
> git reset HEAD~;
OR
> git reset --mixed HEAD~;
```

Option 3 : Undo the commit and completely remove all changes

> git reset --hard HEAD~;

[Source](https://bytefreaks.net/programming-2/how-to-undo-a-git-commit-that-was-not-pushed)

