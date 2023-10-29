
## Intro

Great hardware but limited with crappy software and piss poor app. I regularly have issues of `Internet not connected` or weird issues with FireTV 4K Max Home theatre setup or even the basic Stereo sound setup.
I have 6+ Echo smart speakers and I was gonna upgrade to full studio speakers but screw amazon making it dumb and pushing me notifications and headsup stuff.


## Bad UX | Predatory Upsells

Even with `Do Not disturb` or `Brief mode` this piece of hardware is so bad at respecting your privacy

## Privacy

There's none. It will try to scan all your local devices and probably report it to the big brother for upselling stuff on Amazon or recommendation based on that.
Thankfully I have [pi_hole](pi_hole.md) but its a cat and mouse game with 
these devices


## IOT

Excellent hardware for the price, motion sensor, temperature sensor, low latency zigbee support and future mesh network support `Matter` probably. You can use these speakers for dumb speaker and occasional music playback. I like them for reporting temperature of the house in different rooms to [home_assistant](home_assistant.md)
## Issues


### Weird stereo connection issues

Plus Alexa echo devices when working in Stereo mode kind of communicates with each other on local wifi hotspot and bluetooth option. Plug spotify alexa sends left and right channels streams independently via internet for each devices and then it does the calibration of syncing up. Great technology but lot of things can go wrong.


### Different wifi connections changing. 
Best to forget all old wifi's SSIDs

### 2.4Ghz vs 5Ghz

Sometimes the paired stereo or home theatre setup connects to 2.4ghz and other pair connects to 5Ghz. So it has problem to work in stereo or TV mode.
Best solution is to just turn off smart switch in your wifi router settings if there's an option. Or else just keep default 2.4Ghz to avoid other issues.

### Mesh & Eero

Eero mesh setup with Echo 4th Gen work great but every once in a while with router mode has issues. Eero doesn't give full option to hard code its devices to set a specific wifi channel. Being the Wifi 6 router you have 2.4ghz, 5Ghz - 1 and 5Ghz - 2 bands. Shit's crazy with IPV4 let alone with IPV6 problems.


