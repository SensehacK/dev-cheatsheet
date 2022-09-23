# Certificate

## Guide

App Signing and Provisioning profile for build environment.

Prerequisites

* Personal iOS device
* USB cable
* Admin access
* Keychain Access
* Xcode
* iTunes
* [Apple account](https://developer.apple.com) 

So you may encounter this error when Xcode starts building the project after you have completed all of the steps of Build.

```text
Xcode couldn't find any provisioning profiles matching TeamID/WearWorks Development'. Install the profile (by dragging and dropping it onto Xcode's dock item) or select a different one in the Signing & Capabilities tab of the target editor.
```

### App Signing

iOS apps, even in development environments, in order to run on actual devices requires the app to be digitally signed by a certificate.

This could be fixed easily via getting your own signing certificate.

1. You would need to request your personal apple ID grant access to certain privileges in order to generate your public - private certificate signed by Apple Certificate Authority. Get this from the lead developer or project manager.
2. Open Spotlight \(Command + Space\) -&gt; “Keychain Access” in order to generate a certificate from your own dev mac machine. Go to “Keychain Access” context menu  -&gt; Certificate Assistant -&gt; Create a certificate \(Request a Certificate from Certificate Authority\).
3. Certificate creation window will pop up, enter your information accordingly as the email address should be the one which would be used for signing apps & developer account requested step \#1. Select Request is : “Saved to disk” , “CA email address” should be empty as we are gonna cross sign our certificate with Apple developer CA on their website in next steps.
4. In the Apple developer account portal, select “Create a New Certificate” -&gt; Check “iOS App Development” option. In upload a certificate signing request, choose the cert file created in step \#3.
5. It will process and give you an option to download. Double click the file and it should automatically add it to Keychain Access. You can double check whether the certificate you created is added, it should by default expire after 1 year from the time it is created.

You’re done with creating your own signing certificate signed by Apple CA.

