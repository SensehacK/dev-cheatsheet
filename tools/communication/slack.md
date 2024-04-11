
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

## Disable Slack updates

Just disable this host on your firewall to never connect to their subdomain for checking updates.

```text
https://downloads.slack-edge.com/

// Actual URL of a macOS installer
https://downloads.slack-edge.com/releases/macos/4.36.138/prod/universal/Slack-4.36.138-macOS.dmg
```


## Workflows 

Create workflow in slack. 
[Slack help document](https://slack.com/help/articles/360041352714-Create-workflows-that-start-with-a-webhook)

## Creating quick meetings / event

[Outlook for Slack automation](https://slack.com/help/articles/360020134853-Microsoft-Outlook-Calendar-for-Slack)