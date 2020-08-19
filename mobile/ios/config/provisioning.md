# Provisioning

Provisioning profile is needed for making sure that the signed iOS app should run according to certain privileges or restrictions. For example if an app requires to have “Apple Pay” functionality in their app they need to define that parameter while creating a provisioning profile. By the time of reading this, usually the provisioning profile should be already set up by lead developers, you would only need it specifically if you want to add any new capability which Apple offers or want to run the signed iOS app on your personal devices.

## Prerequisite

You would need to get the UUID of your personal device from iTunes when the iOS device is connected through “Wifi” or “Wired”. \([Guide](https://www.imore.com/how-find-your-iphones-serial-number-udid-or-other-information)\)

Copy the UUID and send it to your lead developer or manager who is managing the provisioning profile creation.

## Steps

1. The person will log in to the Apple Developer portal. Click on “Generate a Provisioning Profile” -&gt; Select the newly generated Signing Certificate we created in “App signing” step.
2. Next he will select the devices needed for this provisioning profile to work on, usually we can “Select All” and Continue with naming the provisioning profile.
3. Click the “Generate” and ”Download” button, then the shared provisioning profile “Provising\_profile\_name.mobileprovision” could be dragged to Xcode IDE.
4. You may need to quit Xcode and run it again. If for some reason it isn’t still picking up the provisioning profile. You can navigate to Project settings -&gt; “Build Settings” -&gt; Search for “Signing”.
5. Select “Code Signing Identity, Make sure all of those schemes have the appropriate certificate selected with “iOS Development” for Debug and “iOS Distribution” for Release.
6. Same with “Provisioning Profile” -&gt; for each scheme, appropriate certificates are selected. The project is all done using “manual” code signing style.

