
Setting environment variables on the project and reading from them via Terminal.


### Setting variables

```bash
export TEST_RUNNER_QAENV=EnvironmentQA1
```

### Removing Environment variable

```bash
unset variablename 
```
[how-to-set-list-and-remove-environment-variables-in-linux](https://www.cloudbooklet.com/how-to-set-list-and-remove-environment-variables-in-linux/)


## Terminal

You would need to either set the environment variable using 
```bash
export IS_CI_SERVER="false"

// Confirm your environment variable works
echo $IS_CI_SERVER
```

You could also define an `.env` file to source these kind of variables and your project or any kind of host runner needs to include this step as a script before executing the `xcode-build`


## Sourcing Env 

```bash
source .env
```


## List Environment Variables

A list of all the environment variables that are set is displayed in the Terminal or shell window.
```sh
printenv
```
