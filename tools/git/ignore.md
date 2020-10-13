# Ignore

## Template

Generate git ignore files for your project, usually frameworks & libraries like angular, ionic, react usually generate .gitignore file with their generate project cli tool.

[Git Ignore](http://gitignore.io)

## Banishing DS Store

Remove existing files from the repository:

```text
find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch
```

Add the line

.DS\_Store

to the file .gitignore, which can be found at the top level of your repository \(or created if it isn't there already\). You can do this easily with this command in the top directory

```text
echo .DS_Store >> .gitignore
```

Then

```text
git add .gitignore
git commit -m '.DS_Store banished!'
```

[StackOverflow Answer](https://stackoverflow.com/a/107921)

## Untrack Tracked files

Untrack files already added to git repository based on .gitignore [Untrack files gitignore](http://www.codeblocq.com/2016/01/Untrack-files-already-added-to-git-repository-based-on-gitignore/)

## Ignore Specific Filename

Good article on specifics of ignoring filename and their wildcard patterns.

[Git Ignore ](https://linuxize.com/post/gitignore-ignoring-files-in-git/)

