# Sync Fork

Many times you would like to fork a project and work on some changes. After some time, there would be updates on main project and you would like to get the updated build also on your already forked repo.

Fear Not!

[SO Link](https://stackoverflow.com/questions/7244321/how-do-i-update-a-github-forked-repository#7244456)

## Remote

Add the remote, call it "upstream":

> git remote add upstream [https://github.com/whoever/repo.git](https://github.com/whoever/repo.git)

## Fetch

Fetch all the branches of that remote into remote-tracking branches, such as upstream/master:

> git fetch upstream

## Master Branch

Make sure that you're on your master branch:

> git checkout master

## Options

### Rewrite

Rewrite your master branch so that any commits of yours that aren't already in upstream/master are replayed on top of that other branch:

> git rebase upstream/master

Disadvantage: Force push to Github using -f flag & also you would rewrite the git history for others who may have cloned your fork.

### Merge

Merge your master branch with upstream/master branch but for future PRs to be clean as possible without excess merge commits, Rebase is the option.

> git merge upstream/master

Disadvantage: Extra merge commits which could lead to less cleaner git history.

[Official Github Doc](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)

