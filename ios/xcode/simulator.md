# Simulator

## Location

It can be simulated on iOS simulator for specific lat and long or some predefined physical locations.

Xcode -> `Project-Scheme` -> `Edit Scheme` -> `Run(Debug)` -> `Options` 
Core Location -> `Allow Location Simulation`
You can provide your custom `.gpx` coordinates to emulate that specific Latitude & Longitude if needed.
You can even simulate walking or moving coordinates. That location file format has different ways of simulating advance locations.

But this all depends on how the app or service tracks your location, some only take your word for it - like GPS coordinates, some correlate that data with `IP addresses`, some have VPN known addresses in their blocklists. Some do device discovery for eg. Home Alexa + Google Android devices which all share their IP addresses or GPS coordinates to their mothership. Which averages out their data to fizzle out your `spoofed` location data for accessing their geo-location specific content. It's a cat and mouse game with `geotracking` APIs.

![](xcode-location-spoofing.png)
## API Support

### Mail

Some functionality while running an app in iOS simulator won’t work due to the limited access on simulator.

For eg.

```x-callback-url
mailto:
```
## Mind Map

[deep linking](ios/config/linking.md)

[compiler directives wildcard_checks for iOS Simulator](ios/library/wildcard_checks#Check%20Simulator)


API won’t work on simulator for opening email client with method called `-canOpenURL` with an error message thrown in console saying “error: "This app is not allowed to query for scheme mailto"


## Commands

Erasing the simulator of iOS via xcode CLI

```sh
sudo xcrun simctl erase all
```

Shutting down simulators

```sh
xcrun simctl shutdown all
```

## Health

Health data continuous workout randomized data could be accessible for testing the app.

Health app doesn’t fully synced my data to the iOS simulator. Or maybe I was missing some iCloud sync settings. I did turned on Health explicitly on “Settings” app of the simulator.

## Offline Mode

Utilize the network link conditioner on Mac OS.
[Network disable](https://www.tutorialspoint.com/how-to-disable-the-network-in-ios-simulator)

Test your iOS application by simulating a bad network connection with Network Link Conditioner
[simulate-a-bad-network](https://designcode.io/swiftui-advanced-handbook-simulate-a-bad-network)


## Directories

[avanderlee | Xcode Simulator Directories Exploration](https://www.avanderlee.com/xcode/simulator-directories-access/)

### Screenshot location

I just hate screenshots default location on Desktop where my wallpaper is 100% digital black as my main coding screen is OLED TV 48 LG C1.
So when coding I like to use 21:9 aspect ratio to get wide screen effect and having that lingering screenshots just feels not right.

Storing the default location 
```bash
defaults write com.apple.iphonesimulator ScreenShotSaveLocation -string ~/Documents/Screenshots
```

[Good reference for Mac OS defaults](https://macos-defaults.com/simulator/screenshotsavelocation.html)
[SO | change-the-location-of-screen-shots-saved-by-the-ios-simulator](https://stackoverflow.com/questions/23661097/change-the-location-of-screen-shots-saved-by-the-ios-simulator) 

## Architecture

**_iOS Platforms:_**

- iOS device `"generic/platform=iOS"`
- Simulator `"generic/platform=iOS Simulator"`

**Note:** There a whole lot more platforms. For brevity I’m just focused on iOS platforms. Otherwise there are macOS, watchOS, tvOS, visionOS platforms.

**_CPU Architectures:_**

- arm64
- x86_64


## find simulator Identifier

Go in Xcode status bar -> Window -> Organizer and Simulators
Check the simulator and copy the ID.




## Errors


### loaded CoreSimulatorService is no longer valid

```text
loaded CoreSimulatorService is no longer valid for this process.  Simulator services will no longer be available.  Error=Error Domain=NSPOSIXErrorDomain Code=61 "Connection refused" UserInfo={NSLocalizedDescription=CoreSimulator.framework was changed while the process was running.  This is not a supported configuration and can occur if Xcode.app was updated while the process was running.  Service version (944.5) does not match expected service version (942).}
Domain: NSPOSIXErrorDomain
Code: 61

```


### failed to launch

```log
Failed to start launchd_sim: could not bind to session, launchd_sim may have crashed or quit responding
Domain: com.apple.SimLaunchHostService.RequestError
Code: 4
```


delete the simulator cache 

```sh
sudo rm -rf ~/Library/Developer/CoreSimulator/Caches
```