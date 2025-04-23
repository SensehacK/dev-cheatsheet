# Rebase

Most of the time I use interactive rebase option or else use a GUI for doing a rebase.

Tower - Git app really helps to do rebase properly and gives more context to what is happening on the first instance.


## Commands

Use [`git rebase`](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase). For example, to modify commit `bbc643cd`, run:

```bash
git rebase --interactive bbc643cd~
```

Please note the tilde `~` at the end of the command, because you need to reapply commits on top of the previous commit of `bbc643cd` (i.e. `bbc643cd~`).

In the default editor, modify `pick` to `edit` in the line mentioning `bbc643cd`.

Save the file and exit. git will interpret and automatically execute the commands in the file. You will find yourself in the previous situation in which you just had created commit `bbc643cd`.

At this point, `bbc643cd` is your last commit and you can [easily amend it](https://www.atlassian.com/git/tutorials/rewriting-history#git-commit--amend). Make your changes and then commit them with the command:

```bash
git commit --all --amend --no-edit
```

After that, return back to the previous HEAD commit using:

```bash
git rebase --continue
```

**WARNING**: Note that this will change the SHA-1 of that commit **as well as all children** -- in other words, this rewrites the history from that point forward. [You can break repos doing this](https://stackoverflow.com/a/3926832/1269037) if you push using the command `git push --force`.


Copied from - [SO | post](https://stackoverflow.com/a/1186549/5177704)

## Reference

Merging vs Rebasing
https://www.atlassian.com/git/tutorials/merging-vs-rebasing