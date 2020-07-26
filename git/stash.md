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
