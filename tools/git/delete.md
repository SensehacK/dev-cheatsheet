# Delete

## Last local commit

If you have committed some files and still not pushed to cloud git server you can still hard reset the head to remove that commit and history too.

> git reset --hard HEAD^

Also next git push won’t commit the deleted commit and also you will lose the commit changes progress so make sure you have your work stashed or saved off to some folder or file.

[Stack Overflow](https://stackoverflow.com/questions/8903953/how-to-revert-last-commit-and-remove-it-from-history)




## For reverting Undo the commits.

Removing the last commit from the git current branch 
> git reset --soft HEAD~1  

[SO](https://stackoverflow.com/questions/3197413/how-do-i-delete-unpushed-git-commits)