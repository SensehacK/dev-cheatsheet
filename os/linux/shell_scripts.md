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


[Source](https://www.cyberciti.biz/faq/run-execute-sh-shell-script/)


## Escape space characters

I've solved it by including a backslash to escape the space:
/Program Files` becomes `/Program\ Files`

```bash
DESTINATION_PLATFORM_VALUE="generic/platform=iOS Simulator"
# vs
DESTINATION_PLATFORM_VALUE="generic/platform=iOS\ Simulator"
```



https://stackoverflow.com/questions/5819423/bash-variables-with-spaces
