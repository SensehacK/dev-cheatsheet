
## Patch


[git man page](https://git-scm.com/docs/git-apply)


Creation


search summary copied
> To create a Git patch, use `git diff` to generate the changes and redirect the output to a file. For instance, `git diff > my_patch.patch` creates a patch file named `my_patch.patch` containing the differences between the current working directory and the last commit. You can also create patches from specific commits using `git format-patch` or between two branches using `git diff branch1..branch2`

```sh
git diff > some-changes.patch
# OR
git diff > patch.diff
```

Applying 

```sh
git apply /Users/patch.diff
```

[SO | post](https://stackoverflow.com/questions/2249852/how-to-apply-a-patch-generated-with-git-format-patch)

