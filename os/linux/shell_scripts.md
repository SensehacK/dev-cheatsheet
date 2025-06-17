# Shell Scripts


## Execute

How do I run .sh file shell script in Linux?

The procedure to run the .sh file shell script on Linux is as follows:

- Open the Terminal application on Linux or Unix

- Create a new script file with .sh extension using a text editor

- Write the script file using nano script-name-here.sh
    Set execute permission on your script using chmod command :
    chmod +x script-name-here.sh

- To run your script :
    ./script-name-here.sh
    Another option is as follows to execute shell script:
    sh script-name-here.sh
    ORbash script-name-here.sh

[run-execute-sh-shell-script](https://www.cyberciti.biz/faq/run-execute-sh-shell-script/)

## Escape space characters

I've solved it by including a backslash to escape the space:
/Program Files` becomes `/Program\ Files`

```bash
DESTINATION_PLATFORM_VALUE="generic/platform=iOS Simulator"
# vs
DESTINATION_PLATFORM_VALUE="generic/platform=iOS\ Simulator"
```


[SO | bash-variables-with-spaces](https://stackoverflow.com/questions/5819423/bash-variables-with-spaces)




## Run on Startup

Try using this command to ensure your script is added to the boot sequence:

```sh
sudo update-rc.d /etc/init.d/nameofscript.sh defaults
```

Note that you can make a script executable using the +x option with chmod:

```sh
chmod +x /etc/init.d/nameofscript.sh
```

[run-bash-script-on-startup](https://raspberrypi.stackexchange.com/questions/15475/run-bash-script-on-startup)







## Assignment

Cannot have spaces around `=` sign

```error
Unexpected arguments:
command not found
```

```bash
built_device =`$device`
built_device = `$device`
built_device=`$device`
```

When you write:
```bash
STR = "foo"
```
bash tries to run a command named `STR` with 2 arguments (the strings `=` and `foo`)

```bash
STR =foo
```
bash tries to run a command named `STR` with 1 argument (the string `=foo`)

```bash
STR= foo
```
bash tries to run the command `foo` with STR set to the empty string in its environment.

[copied from SO | great answer](https://stackoverflow.com/questions/2268104/command-not-found-error-in-bash-variable-assignment)




## variables

```sh
foo="something"
bar="foo"
echo "${!bar}"

# something
```

[SO | bash variable variables](https://stackoverflow.com/questions/10757380/bash-variable-variables)


## eval

```bash
x="ls | wc"
eval "$x"
y=$(eval "$x")
echo "$y"
```

[SO | store a command in a variable in a shell script?](https://stackoverflow.com/questions/5615717/how-can-i-store-a-command-in-a-variable-in-a-shell-script)
