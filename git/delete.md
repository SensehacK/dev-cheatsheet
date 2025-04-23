# Delete

## Last local commit

If you have committed some files and still not pushed to cloud git server you can still hard reset the head to remove that commit and history too.

```sh
git reset --hard HEAD^
```
	
Also next git push won’t commit the deleted commit and also you will lose the commit changes progress so make sure you have your work stashed or saved off to some folder or file.

[Stack Overflow](https://stackoverflow.com/questions/8903953/how-to-revert-last-commit-and-remove-it-from-history)


## For reverting Undo the commits.

Removing the last commit from the git current branch 
```sh
git reset --soft HEAD~1 
``` 

[SO](https://stackoverflow.com/questions/3197413/how-do-i-delete-unpushed-git-commits)

## Options

Multiple options if we haven’t pushed the code to origin server.

Option 1 : Undo commit and keep all files staged

```sh
git reset --soft HEAD~;
```

Option 2 : Undo commit and un-stage all files

```sh
git reset HEAD~;
# OR
git reset --mixed HEAD~;
```

Option 3 : Undo the commit and completely remove all changes

```sh
git reset --hard HEAD~;
```

[Source](https://bytefreaks.net/programming-2/how-to-undo-a-git-commit-that-was-not-pushed)


## Revert Range history

If your changes have already been pushed to a public, shared remote, and you want to revert all commits between HEAD and `<sha-id>`, then you can pass a commit range to git revert,

```sh
git revert 56e05f..HEAD
```

and it will revert all commits between 56e05f and HEAD (excluding the start point of the range, 56e05f).

[SO | revert-to-a-commit-by-a-sha-hash-in-git](https://stackoverflow.com/questions/1895059/revert-to-a-commit-by-a-sha-hash-in-git)


## Delete till a point

If you want to go back to that commit before you made git merge commit you can specify the sha code to make the HEAD to that point.
Eg. SHA: 4e8a118f

```sh
git reset --hard $GIT_COMMIT_SHA
```
[SO | undo-a-git-merge-that-hasnt-been-pushed-yet](https://stackoverflow.com/questions/2389361/undo-a-git-merge-that-hasnt-been-pushed-yet)  
