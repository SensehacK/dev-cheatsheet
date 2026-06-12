
## Patch


[git man page](https://git-scm.com/docs/git-apply)


## Creation

### Diff | Unstaged files

search summary copied
> To create a Git patch, use `git diff` to generate the changes and redirect the output to a file. For instance, `git diff > my_patch.patch` creates a patch file named `my_patch.patch` containing the differences between the current working directory and the last commit. You can also create patches from specific commits using `git format-patch` or between two branches using `git diff branch1..branch2`

```sh
git diff > some-changes.patch
# OR
git diff > patch.diff
```


### Commit Hash

AI (gemini)

**Generate the patch file:** Once you have the commit hash (e.g., `abcd1234`), run the following command. The `-1` flag ensures only that single commit is included
```sh
git format-patch -1 <commit_hash>
```


### Output flag

AI (gemini)
**Specify output location or standard output:**

- To save the patch to a specific directory, use the `-o` flag: `git format-patch -1 <commit_hash> -o <directory_name>`.
- To output the patch content to standard output (e.g., to pipe it elsewhere or save with a custom name), use the `--stdout` option: `git format-patch -1 <commit_hash> --stdout > my-patch.patch`.

## Applying 

```sh
git apply /Users/patch.diff
```

```sh
git am ~/cdn_CAT_patch.diff
```

[SO | post](https://stackoverflow.com/questions/2249852/how-to-apply-a-patch-generated-with-git-format-patch)



## Github 

quick hack

**From GitHub web interface:** You can quickly get a patch for a commit by appending `.patch` to the commit's URL in your web browser.

```sh
https://github.com/company/apple/commit/45f13c266a6cd677fa949b7dfa15a6cd83d56126.patch
```

