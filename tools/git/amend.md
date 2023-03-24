# amend



## Amend author

If you want to change the author details of the commit message, you can do it using flag `--amend`

> git commit --amend --author="Kautilya <kautilya@email.com>"

> git commit --amend --author="Kautilya <kautilya.save@product_name.com>"

[Tower author change](https://www.git-tower.com/learn/git/faq/change-author-name-email/)

[SO](https://stackoverflow.com/questions/3042437/how-to-change-the-commit-author-for-one-specific-commit)


## Change Timestamp


This only works for the last commit in the git history tree.
```bash
git commit --amend --date=now
```

https://stackoverflow.com/questions/454734/how-can-one-change-the-timestamp-of-an-old-commit-in-git