# GitIgnore



## Banishing DS Store




Remove existing files from the repository:

find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch

Add the line

.DS_Store

to the file .gitignore, which can be found at the top level of your repository (or created if it isn't there already). You can do this easily with this command in the top directory

echo .DS_Store >> .gitignore

Then

git add .gitignore
git commit -m '.DS_Store banished!'

[StackOverflow Answer](https://stackoverflow.com/a/107921)

