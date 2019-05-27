# Git Commands

Various Git commands handy cheatsheet.

## List Git Config

List outs all of the git config settings for the particular user.
> git config --list

## Email Git config

Setting your email address for every repository on your computer
Open Terminal.
Set an email address in Git. You can use your GitHub-provided no-reply email address or any email address.
git config --global user.email "email@example.com"

Confirm that you have set the email address correctly in Git:
git config --global user.email
email@example.com

Add the email address to your GitHub account by setting your commit email address on GitHub, so that your commits are attributed to you and appear in your contributions graph.

Setting your email address for a single repository
You can change the email address associated with commits you make in a single repository. This will override your global Git config settings in this one repository, but will not affect any other repositories.
Open Terminal.
Change the current working directory to the local repository where you want to configure the email address that you associate with your Git commits.
Set an email address in Git. You can use your GitHub-provided no-reply email address or any email address.
git config user.email "email@example.com"

### Verify the Git Config

To know the username, type:

> git config user.name

To know the email, type:

> git config user.email
email@example.com

Confirm that you have set the email address correctly in Git:

### Option 1: Enter Git commands

Add the email address to your GitHub account by setting your commit email address on GitHub, so that your commits are attributed to you and appear in your contributions graph.

> \$ git config user.email kautilya.n.save@kns.com
> \$ git config user.email kautilya.save@kns.com

> \$ git config user.email kautilyasave@gmail.com

### Option 2: Edit config file directly

Your other option is to edit the repo config file directly. With a default Git clone, it's usually the .git/config file in your repo's root folder. Just open that file in an editor and starting adding your settings, or invoke an editor for it at the command line using git config --edit.

## Git Stash Commands

Git stash commands comes in handy when needed to pull other branches & the other branch codebase has conflicts with your own branch. This stash utility saves a local copy of your working branch & pulls the new branch & then you can override your local branch with the incoming branch.

> \$ git stash
> \$ git pull --rebase
> \$ git stash apply


## Git Branch Commands

If you want to switch to different branch from your current local uncommitted branch you could follow these steps overall.

Step 1 : Local_Branch_Name (Local Changes) Considering you want to save or forward these changes to your new branch.

Step 2 : Create your newly created branch with base as of updated master or develop.

Step 3 : Run Git stash command to save your workflow.
> \$ git stash
> \$ git checkout branch_name

Step 4 : After switching to new branch via Git CLI or Git GUI just run Stash Apply command for overwriting your changes to new branch.

> \$ git stash apply

## Git Rebase Commands
