# Ionic Packaging 


## Intro
Build and Deploy ionic codebase to a full fledge Web wrapper on target Operating Systems like iOS, Android or even Web App.

This doc contains deploying Ionic application on DevApp, Ionic lab and Xcode so far.
I would add more to this documentation depending on whether I get time to work on that specific process. This doc contains my personal notes while packaging process of Ionic framework.




## DevApp

Make build using Dev App dependency.

First add cordova prepare as it would give build errors for DevApps as their assets or dependencies are still not loaded yet.

> ionic cordova prepare

Ionic serve for ip address usage on Devapp
> ionic serve -c
> ionic serve —devapp


Add IP address manually if the app isn’t showing up on the Ionic DevApp.

Debugging Tips:
Use manual IP address and make sure the port is right.


## iOS Build

### Build process for iOS Xcode project

Great documentation for easy reference if anything is obsolete for my doc.
[Official Documentation](https://ionicframework.com/docs/v3/intro/deploying/)

P.S Everything would be obsolete with hybrid app development as the framework and libraries change too frequently.

First add cordova package globally in CLI
Add Cordova package globally
> $ npm install -g ionic cordova
Then run these commands as per requirement

This commands adds iOS platform to the project structure & it comprises of Xcode build files.
> $ ionic cordova platform add ios

Command for Xcode build Cordova
This command would build the project using Xcode-build CLI tools
> $ ionic cordova build ios

Command for building app with production flag
> $ ionic cordova build ios --prod




## WebApp Build


Make prod build using the following command to create a www directory.

> ionic build --prod

The ‘www’ folder would contain parsed or compiled typescript converted code into minimized javascript for small builds and easy parsing for browsers.


Also edit the ‘index.html’ file for referencing the whole web app to root directory.


> <base> tag to <base href="." />


## Deploy Firebase

> ionic build —prod —release

To make the release build for minimizing the build file.
