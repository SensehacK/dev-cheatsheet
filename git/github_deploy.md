

## Deploy branch


```log
Branch "debugging" is not allowed to deploy to github-pages due to environment protection rules.
```

update the env protection rule to match default branch and deployment worked.
this can be done by visiting settings for your repo, then "Environments", then "github-pages", then changing the allowed branch.

