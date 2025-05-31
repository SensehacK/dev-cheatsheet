
# Vision Pro Development Experience


## Developer mode

On the Vision Pro:

- Go to Settings > General > Remote Devices and select your computer

On your Mac:

- Go to Xcode > Window > Devices and Simulators
- Find your Vision Pro in the Devices list on the left
- Pair your Vision Pro using the code seen in the Settings app in Vision Pro

## Simulator


## Physical AVP

It's bit hard to navigate with 2 wires on both sides of the AVP. 
I still don't have accurate prescription so I can't see properly on the actual macOS, iPhone displays. The text isn't that crisp or maybe vision Pro passthrough wont be able to handle that much small text or thin font sizes.

I'll check on connecting the macOS desktop to vision pro, would i need to update my macOS, I hope not.


Had to do the normal provisioning of new Apple hardware using the developer account with xcode 15.2 & my dev IDs.



## Changing Users


- Say "Siri, enroll hands."
- Go to Settings > Eyes & Hands, then tap Redo Hand Setup.
- Or press action button 4 times to start eye tracking calibration
- Screen lens placement - more spaced out or near each other.

## Multi Tasking

### How to force quit an app in visionOS on Apple Vision Pro

1. Press and hold both the **top button** and the **Digital Crown**. Keep the button and dial **held down** until the **Force Quit Applications window appears** on-screen, then **release** the buttons.
2. In the Force Quit Applications window, select the **app** that you wish to close. Once selected, a checkmark will be displayed next to the app's icon.
3. Select **Force Quit**.
4. Confirm the action by selecting **Force Quit** again.

## Sideloading

Refer to this page I maintain for all apple related side loading or resigning needs.
[VisionOS sideload](/ios/config/resigning#visionOS)




## TODO


- Sideload apps
- PlexKit
- Video player (https://www.hackingwithswift.com/quick-start/swiftui/how-to-play-movies-with-videoplayer)
- [3D Movie MV-HEVC](360_Video.md#3D%20Video)
- Play around with ornaments
- play with immersive environment
- connect trakt tv api
- trakt tv watchlist and plex to watch the movie / stream the movie
- connect with friends
- show where to watch the watchlist movie (using Where to watch movie / tv show api)
- share a message to your friend on imsg
- Shareplay integration




## Plex Kit


https://support.plex.tv/articles/201638786-plex-media-server-url-commands/

https://www.reddit.com/r/PleX/comments/12dy7hv/announcement_open_source_plex_api_documentation/

https://github.com/topics/plex-api


https://github.com/lcharlick/PlexKit?tab=readme-ov-file



## Dark Mode visionOS

[low-hanging-fruit-for-ios-apps-running-on-visionos-](https://medium.com/@timonus/low-hanging-fruit-for-ios-apps-running-on-visionos-08a85db0fb31)


## WebKit

https://webkit.org/blog/15063/webkit-features-in-safari-17-4/



## Battery

It seems the AVP I charged 2 days ago lost its charge or something. Had to refer to this doc about the various charging color blinking states.
Maybe I had it connected to the macbook with cable it discharged itself ? dont know but excited to run the app on actual AVP.

Oh after ~8 mins - it chimes loudly stating that it has booted up. Nice UX indeed, so you don't have to put it on and wait for the display to turn on or not.

### States

[Apple support article](https://support.apple.com/en-us/117740) 
- Green for several seconds: the battery is charged to 50% or higher.
- Amber for several seconds: the battery's charge level is between 5% and 49%.
- Amber pulsing slowly: the battery's charge level is too low to power your Apple Vision Pro. Charge the battery for 10 minutes, or until the light shows amber steadily (not pulsing) when you tap the battery.

## No Multiple Profiles support

I still hate how apple hasn't added multiple user / profiles option on their iPad (home device). That would be really cool to have but I assume it will cannibalized their own device sales.
[Reddit thread](https://www.reddit.com/r/AppleVisionPro/comments/1ai4re3/no_multiple_profile_support_is_a_seriously_flawed/)

They do support them on Apple TV and macOS (for quite some time).
[apple tv switch users](https://support.apple.com/guide/tv/switch-users-in-the-profiles-tab-atvb5f549664/tvos)



## Errors


