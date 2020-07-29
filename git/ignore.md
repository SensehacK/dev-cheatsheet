# Git Ignore

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

