# OS Quirks

## Audio Service

Sometimes macOS doesn’t detect my audio device like “AirPods Pro” or Google Mini speaker. Even when manually switching the audio output doesn’t fix it. Restarting fixes it but that is very cumbersome.

We can just kill the audio service and restart it automatically using the following command.

```sh
sudo kill -9 `ps ax|grep 'coreaudio[a-z]' | awk '{print $1}'`
```

Enter the password in the terminal and it is done. It should be working fine with the new audio device to switch the audio input and output. [Stack Exchange Link](https://apple.stackexchange.com/questions/16842/restarting-sound-service)

[Restart Services](https://serverfault.com/questions/194832/how-to-start-stop-restart-launchd-services-from-the-command-line)



## Audio Cracking

Macbook pro 16 audio cracking

I have this issue with my Macbook pro 2020, 13 inch , It appears from time to time , there is two solutions: 

1- restart the macbook pro , but when you work it will be annoying sometimes 

2- open activity monitor and quit the `audioid` it works just fine 
[Source](https://discussions.apple.com/thread/251203866)
[Apple forums](https://developer.apple.com/forums/thread/132423)


### App install update popups

Slack Popup saying 
An update is ready to install. Slack is trying to add a new helper tool.
Enter your password to allow this.
```sh
sudo chown -R $USER /Applications/Slack.app
```

Or if you 



## Search with Default browser


Add automator / workflow and set it in default browser
[Stack Exchange | MacOS - system preferences](https://apple.stackexchange.com/questions/10999/search-in-google-always-open-safari-instead-of-default-browser) 


Create a workflow for automator

[super user | create a shortcut for search with google](https://superuser.com/questions/369934/mac-os-x-lion-chrome-shortcut-for-search-with-google) 

maybe try this app but i didn't fully config it to check whether it works perfectly
[Velja macOS app](https://apps.apple.com/ca/app/velja/id1607635845?mt=12)

Location of Automator script.
Automator Quick Actions are saved into /Users/username/Library/Services. By default, Workflows are saved in the **Workflows folder in the local library**