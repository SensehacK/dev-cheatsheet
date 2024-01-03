
## Mind Map

[Work App configuration for Slack](process/work_apps#Slack)

## Revert to classic Slack

[Excellent post from Reddit thread](https://www.reddit.com/r/Slack/comments/16ib0l7/comment/k0kfpc8/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)

I was able to run it on the Mac app but it's only temporary, it reverts next time I open Slack:

- Close the Slack app
- Open the terminal and run these two commands separately

```sh
export SLACK_DEVELOPER_MENU=true
# or 
SLACK_DEVELOPER_MENU=true /Applications/Slack.app/Contents/MacOS/Slack
```

Slack will open with the new theme but now we have access to its console
```sh
open /Applications/Slack.app
```

- Open Slack's developer console by pressing `command + option + I`
- Run this in Slack’s chrome developer console command - thank you `Electron` chromium wrapper to deliver apps and access web storage commands.

```sh
localStorage.setItem("localConfig_v2", localStorage.getItem("localConfig_v2").replace(/\"is_unified_user_client_enabled\":true/g, '\"is_unified_user_client_enabled\":false'))
```

- Restart slack with `command + R`