# Merge

## Squash And Merge

[SO Link](https://stackoverflow.com/questions/5308816/how-to-use-git-merge-squash)

Say your bug fix branch is called bugfix and you want to merge it into master:

```text
git checkout master
git merge --squash bugfix
git commit
```

This will take all the commits from the bugfix branch, squash them into 1 commit, and merge it with your master branch.

### Explanation:

```sh
git checkout master
```

Switches to your master branch.

```sh
git merge --squash bugfix
```

Takes all the commits from the bugfix branch and merges it with your current branch.

```sh
git commit
```

Creates a single commit from the merged changes.

Omitting the -m parameter lets you modify a draft commit message containing every message from your squashed commits before finalizing your commit.



## [Merge Restrictions](peer_review.md#Restrictions%20PR%20MR%20Rules) 

## [Xcode Merge](xcode_merge.md)
