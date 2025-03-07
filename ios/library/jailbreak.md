# Jailbreak

## Mobile Substrate

Getting started with Mobile Substrate tweaking.

[SO | mobile substrate tweaks](https://stackoverflow.com/questions/6118814/is-there-anywhere-where-i-could-start-mobilesubstrate-tweaks-programming/11553722)


## Update packages

In terminal type (after logging with su):

```sh
mkdir -p var/cache/apt/archives/partial
apt-get update
```

## Side Loading

You can read more about it in [resigning](resigning.md) and my favorite [third party apps](third_party_apps.md)

## Patched SDK

[github | theos | patched SDK](https://github.com/theos/sdks)


## Inject dynamic lib

GUI tool to inject dynamic libraries into IPA files
[iPatch github](https://github.com/EamonTracey/iPatch)


## Tools

[sideloadly | app signer tool](https://sideloadly.io/)

[github | ios-app-signer](https://dantheman827.github.io/ios-app-signer/)

[altstore](https://faq.altstore.io/)

[trollstore](https://trollstore.app/)(for iOS 15 signing exploit)

[For history of iOS Jailbreaking](https://mega.nz/folder/k4FAXCIB#Fk7pxs6ikYzL3YBvAGX5ig)

[decrypted day  iPAs](https://decrypt.day/)

[Azule](https://github.com/Al4ise/Azule)

A cross-platform suite of tools for building and deploying software for iOS and other platforms.
[theos](https://github.com/theos/theos)

Utility to decrypt App Store apps on jailbroken iOS 11.x
[bfdecrypt](https://github.com/BishopFox/bfdecrypt)




## Modded Apps

### Reddit

Reddit Client Custom Third Party App

-  **Obtain Reddit Client-ID - API Credentials**
```steps
Step 1: Go to [https://reddit.com/prefs/apps](https://reddit.com/prefs/apps) and sign in
Step 2: Click the are you a developer? create an app... button
Step 3: Fill in the fields
name: Use whatever
Choose Installed App
description: can be left blank
about url: can be left blank
redirect uri: `apollo://reddit-oauth`
create app
```

- After creating the app you'll get a client identifier; it'll be a bunch of random characters. That is your API key.
- Install Apollo (w/ApolloPatcher) iPA file on iOS / iPadOS device.
- Enter the Client ID in the settings and tap "Set RedditClientID".

Source code
[Apollo-CustomApiCredentials](https://github.com/EthanArbuckle/Apollo-CustomApiCredentials)


### Youtube Vanced

[YTMusic Ultimate](https://github.com/dayanch96/YTMusicUltimate?tab=readme-ov-file)

[Youtube Music Desktop app with Last fm](https://github.com/th-ch/youtube-music)


### Instagram

[SCInsta](https://github.com/SoCuul/SCInsta?tab=readme-ov-file#general)

### Infuse

Suffuse

## Repos

[ipa Library](https://ipalibrary.net/ipa-library-apps/)

[ios ninja](https://iosninja.io/ipa-library-ios)

## Resources

[r/jailbreak](https://www.reddit.com/r/jailbreak/)

[r/sideloaded](https://www.reddit.com/r/sideloaded/)

[r/AltStore](https://www.reddit.com/r/AltStore/)


## iOS Security Flaws

[core trust | apple](https://worthdoingbadly.com/coretrust/)
