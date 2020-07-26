# Merging two repositories

[Video Source](https://www.youtube.com/watch?v=2JqWvl3HFfQ)

Thank you for the helpful guide/tutorial. I couldn't remember all those commands. So I think it would be useful to sum it up for others here.

1. Check remote origins for main repository

```shell
git remote -v
git remote add <RemoteName> <RemoteURL>
```

2. Fetching the newly added second repo to our main repo file location

```shell
git fetch <RemoteName>
```

3. Check to see whether remote is available with

```shell
git remote -v
```

4. Create a new branch with

```shell
git checkout -b <NewBranchName> <Branch(RemoteName)/master>
```

5. Move all the files into a subdirectory so there aren't any conflicts with names (git mv) and commit the files.
(No need to also move the hidden .git folder in the subdirectory)

```shell
git commit -m "moved"
```

6. If you get any Merge issues like **“Un tracked working tree files would be overwritten by merge”**
You could git stash your branch and merge commit and then git stash apply so that you won’t have any merge conflicts or else you could just commit the files and solve merge conflicts using VSCode / Vim.

```shell
git stash
git stash apply
```

7. Checkout the master branch

```shell
git checkout master
```

8. Merge newly created branch of another repo into the main repo master branch using

```shell
git merge <NewBranchName> --allow-unrelated-histories
```

9. Cleanup everything by removing remote and branch

```shell
git remote rm <RemoteName>
git branch -d <NewBranchName
```

10. Check to see whether everything is correct with

```shell
git remote -v
git branch -a -v
git status
```

11. Push all of these local changes to remote origin

```shell
git push
```

One more Guide [Link](https://thoughts.t37.net/merging-2-different-git-repositories-without-losing-your-history-de7a06bba804)
