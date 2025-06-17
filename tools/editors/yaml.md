
# YAML

## Commands

## Syntax

### Adding comments

single-line YAML
```yaml
# This Deployment runs on our CI machine
kind: Deployment
```


Making inline YAML comments
```yaml
spec:
  retry: 3    # 3 retries will run; this gives us redundancy
```


block YAML
```yaml
# Line 1
# Line 2
# Line 3 
kind: Deployment
```
[yaml comments](https://spacelift.io/blog/yaml-comments)





## Command line tool

yq 

a lightweight and portable command-line YAML processor. `yq` uses [jq](https://github.com/stedolan/jq) like syntax but works with yaml files as well as json.

[yq](https://mikefarah.gitbook.io/yq)