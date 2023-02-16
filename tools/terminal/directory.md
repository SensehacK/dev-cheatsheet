# Directory Commands


## Making directory

> mkdir directory_name


### Make multi level directory

If you want to create directories throughout the whole PATH then you would have to use flag -p

> mkdir -p $HOME/Downloads/Projects2/Internal_Project/Dependency

This will create all the folders/directories necessary till the last folder.




[mkdir and cd](https://linux.101hacks.com/cd-command/mkdir-and-cd-together/)


## Copy directory

> cp -r source_directory_path destination_directory_path

[Linux Handbook](https://linuxhandbook.com/copy-directory-linux/)


## Rename directory

Use move command to rename a directory.

> mv SensehackMedia SensehackMedia2


## Deletion Directories 

Deleting directories using `rm -rf` commands

[remove directory](https://phoenixnap.com/kb/remove-directory-linux)

[Remove dir](https://linuxize.com/post/remove-directory-linux/)

## Check directory exists


```sh
# Checking directories and deciding different paths.
case $PWD/ in
	*/Custom-iOS/Custom-iOS/*)
		echo "🚀🚀🚀"
		. ..ops/dir/script ;;
	*/Custom-iOS/*)
		echo "In previous directory"
		. ops/dir/script ;;
	*)
		echo "❌❌❌ Couldn't find the 'script'. \n Please manually run the setup script! " ;; # default case
esac
```

[SO](https://stackoverflow.com/questions/59838/how-can-i-check-if-a-directory-exists-in-a-bash-shell-script?rq=1)


## Check file exists

If then else approach
Check for git repository being initialized and depending on the condition clone or skip this command. 
```sh
FILE_README=Custom-App/README.md
FILE_GIT=Custom-App/.gitmodules
if [! [ -f $FILE_GIT || -f $FILE_README ]]; then
    echo "Custom-App Main Git Repository already exists."
else 
	echo "Cloning the repository... \nPlease enter your credentials 🔑"
	git clone git@gitlab.com:domain/mobile/Custom-App.git
	cd Custom-App
fi
```


[file exists](https://linuxize.com/post/bash-check-if-file-exists/)


## Loop in directory

We can check for every file or directory in the $PWD & this could be helpful for making automation scripts on a number of files.


[SO](https://stackoverflow.com/questions/2107945/how-to-loop-over-directories-in-linux#2108296)