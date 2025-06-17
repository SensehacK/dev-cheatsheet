
## Use the force luke


```sh
git push --force
```

## Dangers

[SO | post copied](https://stackoverflow.com/a/66087818/5177704)

The main danger when you use `git push --force` is indeed to loose pushed by others developers. So it should not happen.

But you still can loose your own commits by mistake...

As @Prihex mentioned it rightfully in the comments, in this specific case where you loose one of your own commit by mistake, you will still be able to retrieve it by looking at the `git reflog` of the branch that you `git push --force`

PS: Also, be aware that it is a best practice to use `git push --force-with-lease` or `git push --force-if-includes` to reduce the probability to unexpectly loose commits (See [documentation](https://git-scm.com/docs/git-push#Documentation/git-push.txt---force-with-leaseltrefnamegtltexpectgt) )