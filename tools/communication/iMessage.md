
## Backup

[github | imessage - exporter](https://github.com/reagentx/imessage-exporter)

Instructions from reddit thread

Instructions for installing iMessage-exporter for people who don't code:

1.      First install Rust which contains Cargo:  
a.      Open Terminal by going to Finder, Utilities, Terminal  
b.      Type this: 

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh  
```

c.      Hit enter  
d.      Hit enter again when it prompts you if you want to customize or proceed with standard installation  
e.      Close the Terminal window by hitting X (this makes Rust take effect)

2.      Now install the iMesssage-exporter tool  
a.      Reopen Terminal by going to Finder, Utilities, Terminal  
b.      Type this:  This will run for a bit and then throw an error.  
```sh
cargo install imessage-exporter
``` 
c.      You will be asked to install command line developer tools.   
d.      Tap on “install”.  
e.      Tap on “Agree” to the terms and conditions. This install takes a good few minutes so be patient.  
f.       Now go back to that Terminal window and rerun the cargo install:  
g.      Tap on the Terminal, arrow up to bring back the last command, then hit enter.

3.      You are ready to run iMessage-exporter. Note that this will run for a while, depending on how many text messages you have downloaded in the Messages app. In your Terminal window, type this command (where XXXXXX is your Mac username): /Users/XXXXXX/.cargo/bin/imessage-exporter -f html -c compatible 

```sh
/Users/kautilya/.cargo/bin/imessage-exporter -f html -c full
```
Give access to terminal or iterm for `Full Disk access` in macOS -> Settings -> Privacy and Security
4.      To find the exported files, open Finder and navigate to /Users/XXXXXX/imessage_export. They are html files and named after the phone number. Sort them by size to easily locate your top contacts.