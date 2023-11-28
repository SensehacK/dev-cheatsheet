# Config

## Creation of new project

Use this command to create a new project without quotes in command.

> react-native init “project\_name”

## Running the React App

### Environment setup

\(Environment Setup\) \[[https://reactnative.dev/docs/environment-setup](https://reactnative.dev/docs/environment-setup)\]

### Install dependency

We have to install all of the dependencies in the project workspace.

Node Modules dependency installation

> npm install

## iOS

### iOS Dependency

Cocoapods iOS dependency

> pod install

### Xcode iOS Deploy

Run this command on terminal

> react-native run-ios

### Debugging

> npx react-devtools

## Android

Android development guide

### PATH

Add the following lines to your $HOME/.bash\_profile or $HOME/.bashrc config file:

```bash
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

### Check connected devices

> adb devices

### Run Application

> npm run android npx react-native start npx react-native run-android

### Grade Permission

The chmod command sets the permissions of files or directories

> chmod 755 android/gradlew

### Run Application on different port

> npx react-native run-android --port=8080

### To run Emulator from command Prompt

> emulator -avd Android\_pixel

