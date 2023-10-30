


## Git revert merge commit


Excellent post by SO as follows

In `git revert -m`, the `-m` option specifies the **parent number**. This is needed because a merge commit has more than one parent, and Git does not know automatically which parent was the mainline, and which parent was the branch you want to un-merge.

When you view a merge commit in the output of `git log`, you will see its parents listed on the line that begins with `Merge`:

```
commit 8f937c683929b08379097828c8a04350b9b8e183
Merge: 8989ee0 7c6b236
Author: Ben James <ben@example.com>
Date:   Wed Aug 17 22:49:41 2011 +0100

Merge branch 'gh-pages'

Conflicts:
    README
```

In this situation, `git revert 8f937c6 -m 1` will get you the tree as it was in `8989ee0`, and `git revert -m 2` will reinstate the tree as it was in `7c6b236`.

To better understand what you're about to revert do `git diff <parent_commit> <commit_to_revert>`, in this case:

```
git diff 8989ee0 8f937c6
```

and

```
git diff 7c6b236 8f937c6
```

https://stackoverflow.com/questions/7099833/how-do-i-revert-a-merge-commit-that-has-already-been-pushed-to-remote


