# File Permissions



## App Update Helper Password

Mac OS Big Sur has prompts for password every now and then and turns out all you need to do is give access to admin: read/write. Sometimes it's not present in the `Get Info` window and only everyone, user is present and system.

chown is a command to used to change ownership. To change ownership of Slack.app, you'd want to run something like: 

> sudo chown -R $USER:staff /Applications/Slack.app

in a Terminal window. $USER should get replaced by your username automatically, but if it doesn't, just replace it with your computers username.
You can see who the current owner is by running 

> ls -la /Applications/Slack.app

If you see root in there, you probably need to run the command above.

[Reddit Thread](https://www.reddit.com/r/Slack/comments/5l5crw/slack_is_trying_to_install_a_new_helper_tool/)