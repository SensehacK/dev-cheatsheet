
# Mobile Device Management

## Info
Understanding supervision mode on iOS device using MDM profiles setup.
[imazing | understanding-supervision-mdm-ade](https://imazing.com/guides/understanding-supervision-mdm-ade)


## Tools
[iTunes](iTunes.md), Finder, iMazing etc.

## Backup

Local Encrypted backups kinda worked and I didn't have to fully setup my work iOS device again after doing a reset.
Definitely helps having local encrypted backups and restore quickly when `Reset All Content and Erase` option was clicked through and not being paired with local iPhone nearby. Just let it complete little bit and connect the new reset iPhone with Finder / iTunes and just do full restore. After that is done, Apple might ask you to enter the apple ID credentials again to download all the App Store apps but the internal app data is still intact so no need of extra setup needed.

[apple | backup-and-restore-devices](https://support.apple.com/guide/deployment/backup-and-restore-devices-depd44f045b4/web)

[local-backup-of-mdm-managed-iphone](https://community.spiceworks.com/topic/2054454-local-backup-of-mdm-managed-iphone)

[Restoring-iOS-user-data-after-moving-into-the-Automatic-Device-Enrolment-Program](https://support.datajar.co.uk/hc/en-us/articles/206944489-Restoring-iOS-user-data-after-moving-into-the-Automatic-Device-Enrolment-Program)

## Work SSO
### Teams 

iOS app crash for public app store on iOS office phone. It works for first try and then it crashes every time.  Turns out we need to install the app using Company portal on iOS and install the app from internal app store. Probably dealing with some provisioning profile on the physical test or something of that sort which verifies its bundle identifier or something. 

## macOS
### SSO Cant sign in

So if we did macOS compliance check.
Mac company Registration -> Did the Intune `company Endpoint Management`
Microsoft Company Portal

## Disable MDM

[macOS - bypass-mdm](https://github.com/assafdori/bypass-mdm)



## Intune

iOS error codes
[Microsoft FAQs error codes dictionary](https://learn.microsoft.com/en-us/troubleshoot/mem/intune/device-enrollment/profile-installation-failed)