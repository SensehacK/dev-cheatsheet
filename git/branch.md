branch

## Create


The following command will create the branch locally.

```sh
git branch <branch-name>
```

## Name of the branch

Listing out the name of the branch which is checked out without extra information.

```sh
git rev-parse --abbrev-ref HEAD
```


## List branch


With the following command, you can view branch details.

```sh
git branch
```

or
```sh
git branch --list
```

Listing git branches with different options.
```sh
git branch -a - All branches.

git branch -r - Remote branches only.

git branch -l or git branch - Local branches only.
```


## Change branch

This will checkout the branch.

```sh
git checkout -b NEW-BRANCH-NAME
```


## Delete branch

To delete the branch, you can run the command:

```sh
git branch -d <branch-name>
```

## Push branch

Once you create the branch, push it to the remote repository using the command:

```sh
git push -u <remote> <branch-name>
```