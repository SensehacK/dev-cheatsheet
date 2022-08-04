# OS Quirks

## Audio Service

Sometimes macOS doesn’t detect my audio device like “AirPods Pro” or Google Mini speaker. Even when manually switching the audio output doesn’t fix it. Restarting fixes it but that is very cumbersome.

We can just kill the audio service and restart it automatically using the following command.

> sudo kill -9 `ps ax|grep 'coreaudio[a-z]' | awk '{print $1}'`

Enter the password in the terminal and it is done. It should be working fine with the new audio device to switch the audio input and output. [Stack Exchange Link](https://apple.stackexchange.com/questions/16842/restarting-sound-service)

[Restart Services](https://serverfault.com/questions/194832/how-to-start-stop-restart-launchd-services-from-the-command-line)



## Audio Cracking

Macbook pro 16 audio cracking

I have this issue with my Macbook pro 2020, 13 inch , It appears from time to time , there is two solutions: 

1- restart the macbook pro , but when you work it will be annoying sometimes 

2- open activity monitor and quit the `audioid` it works just fine 
[Source](https://discussions.apple.com/thread/251203866)
[Apple forums](https://developer.apple.com/forums/thread/132423)