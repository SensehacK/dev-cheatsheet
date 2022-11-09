# Simulator

## Location

It can be simulated on iOS simulator for specific lat and long or some predefined physical locations.

## API Support

### Mail

Some functionality while running an app in iOS simulator won’t work due to the limited access on simulator.

For eg.

> mailto:

API won’t work on simulator for opening email client with method called `-canOpenURL` with an error message thrown in console saying “error: "This app is not allowed to query for scheme mailto"

### Health

Health data continuous workout randomized data could be accessible for testing the app.

Health app doesn’t fully synced my data to the iOS simulator. Or maybe I was missing some iCloud sync settings. I did turned on Health explicitly on “Settings” app of the simulator.


## Offline Mode


Utilize the network link conditioner on Mac OS.

[Network disable](https://www.tutorialspoint.com/how-to-disable-the-network-in-ios-simulator)


## Screenshot location

I just hate screenshots default location on Desktop where my wallpaper is 100% digital black as my main coding screen is OLED TV 48 LG C1.
So when coding I like to use 21:9 aspect ratio to get wide screen effect and having that lingering screenshots just feels not right.

Storing the default location 
```bash
defaults write com.apple.iphonesimulator ScreenShotSaveLocation -string ~/Documents/Screenshots
```

Good reference for Mac OS defaults
https://macos-defaults.com/simulator/screenshotsavelocation.html

SO https://stackoverflow.com/questions/23661097/change-the-location-of-screen-shots-saved-by-the-ios-simulator