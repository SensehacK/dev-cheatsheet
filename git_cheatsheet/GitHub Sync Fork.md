GitHub Sync Fork


Many times you would like to fork a project and work on some changes. After some time, there would be updates on main project and you would like to get the updated build also on your already forked repo.

Fear Not!

[SO Link](https://stackoverflow.com/questions/7244321/how-do-i-update-a-github-forked-repository#7244456) 


# Add the remote, call it "upstream":

git remote add upstream https://github.com/whoever/whatever.git

# Fetch all the branches of that remote into remote-tracking branches,
# such as upstream/master:

git fetch upstream

# Make sure that you're on your master branch:

git checkout master

# Rewrite your master branch so that any commits of yours that
# aren't already in upstream/master are replayed on top of that
# other branch:

git rebase upstream/master