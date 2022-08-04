# Stash

Stashing changed the way we take upstream changes from different branches or repos. With this command you could easily have your working state saved or stashed in the git stack.

## Basics

You can save the working directory just by doing

> git stash

You can merge the other branches or stuff you need to do.

Then when you need to pop the working state saved on the stack, you can just override the current state with

> git stash apply

Or just pop the stash then

> git stash pop

Workflow difference explanation on [StackOverflow](https://stackoverflow.com/questions/15286075/difference-between-git-stash-pop-and-git-stash-apply?noredirect=1&lq=1)

## Quirks

Some times you would have to stage some files in order to pop the stash from Git.

This thread accurately describes my scenario. [Link](https://stackoverflow.com/questions/19937580/cant-pop-git-stash-your-local-changes-to-the-following-files-would-be-overwri)

## List

You can view your previous stash stored on that repository using this command.

> git stash show -p

## Delete

You can delete the git stash history of a local repository, by running this command

> git stash drop


## Git Stash Commands

Git stash commands comes in handy when needed to pull other branches & the other branch codebase has conflicts with your own branch. This stash utility saves a local copy of your working branch & pulls the new branch & then you can override your local branch with the incoming branch.

```sh
git stash
git pull --rebase
git stash apply
```

## Git Branch Commands

If you want to switch to different branch from your current local uncommitted branch you could follow these steps overall.

Step 1 : Local\_Branch\_Name \(Local Changes\) Considering you want to save or forward these changes to your new branch.

Step 2 : Create your newly created branch with base as of updated master or develop.

Step 3 : Run Git stash command to save your workflow.

```sh
git stash
git checkout branch_name
```

Step 4 : After switching to new branch via Git CLI or Git GUI just run Stash Apply command for overwriting your changes to new branch.

> git stash apply

