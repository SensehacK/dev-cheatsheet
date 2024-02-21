# Tag

## Intro

You can check tags via

```sh
git tag
```

### Note
Sometimes this command makes the terminal go into input mode. Was reproducible on default macOS terminal on my CI build machine running M2 Ultra & macOS Ventura 13.6.
Same git version
git version 2.39.3 (Apple Git-145)

## Creating Tags

Lightweight Tags

```sh 
git tag v1.5
```

Annotated Tags

```sh 
git tag -a v2.0 -m “CS Second Semester”
```


The -m specifies the comment or description for the tag.


## Fetch Tags

```sh
git fetch --all --tags
```

Descending order of latest tags

```sh
git tag --sort=-creatordate
```

## Checkout Tag

Checkout specific tag 

```sh
git checkout tags/6.2.0-rc1-ga -b 6.2.0-branch
```

## Checking HEAD Tag logs

```sh
git log --oneline --graph
```

Make sure the head branch and previous commits have tag in the head just to double confirm.



## Combining Release

## Deleting Tags

Deleting tags is also easy, by default it deletes the local repo branch.

Deleting on local origin Branch

```sh
git tag --delete v0.1
```

Deleting on Remote origin Branch

```sh
git push --delete origin v0.1
```

## Local vs Remote

Tags are available on Local repo and remote repo url. To publish most of the changes or sync with each other, we would need an extra command to be ran in order to update both places.

By default, the git push command doesn’t transfer tags to remote servers. [git basics tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

We need to push tags from local to remote repo, where “v1.5” is tag name.

```sh
git push origin v1.5
``` 


## Resources

[SO create a tag](https://stackoverflow.com/questions/18216991/create-a-tag-in-a-github-repository)

[how to checkout git tags](https://devconnected.com/how-to-checkout-git-tags/)

