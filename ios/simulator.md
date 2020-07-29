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
