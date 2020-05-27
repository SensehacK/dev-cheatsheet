# Git Tag


## Intro

You can check tags via 
> git tag

## Creating Tags

Lightweight Tags
> git tag v1.5

Annotated Tags
 > git tag -a v2.0 -m “CS Second Semester”
 
 The -m specifies the comment or description for the tag.
 
## Combining Release
 

## Deleting Tags

Deleting tags is also easy, by default it deletes the local repo branch.

Deleting on local origin Branch
> git tag --delete v0.1


Deleting on Remote origin Branch
> git push --delete origin v0.1


## Local vs Remote

Tags are available on Local repo and remote repo url.
To publish most of the changes or sync with each other, we would need an extra command to be ran in order to update both places.

By default, the git push command doesn’t transfer tags to remote servers.
[Source](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

 We need to push tags from local to remote repo, where “v1.5” is tag name.
 
 > git push origin v1.5

