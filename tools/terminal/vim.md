# Vim

[Stack Overflow](https://stackoverflow.com/a/11828573/5177704)

Hit the Esc key to enter "Normal mode". Then you can type : to enter "Command-line mode". A colon \(:\) will appear at the bottom of the screen and you can type in one of the following commands. To execute a command, press the Enter key.

:q to quit \(short for :quit\) :q! to quit without saving \(short for :quit!\) :wq to write and quit :wq! to write and quit even if file has only read permission \(if file does not have write permission: force write\) :x to write and quit \(similar to :wq, but only write if there are changes\) :exit to write and exit \(same as :x\) :qa to quit all \(short for :quitall\) :cq to quit without saving and make Vim return non-zero error \(i.e. exit with error\) You can also exit Vim directly from "Command mode" by typing ZZ to save and quit \(same as :x\) or ZQ to just quit \(same as :q!\). \(Note that case is important here. ZZ and zz do not mean the same thing.\)

Vim has extensive help - that you can access with the :help command - where you can find answers to all your questions and a tutorial for beginners.

