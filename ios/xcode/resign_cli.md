# Resign CLI

## Prerequisites

* Xcode IDE
* Mac OS
* iTunes
* iOS Device

## Creation

## Many times we would have different teams to handle app bundle signing from different build configuration.

It's really easy to do from the command line. I had a gist of a script for doing this. It has now been incorporated into the ipa\_sign script in [link](https://github.com/RichardBronosky/ota-tools) which I use daily. If you have any questions about using these tools, don't hesitate to ask.

The heart of it is this:

```text
IPA="/path/to/file.ipa"
PROVISION="/path/to/file.mobileprovision"
CERTIFICATE="Name of certificate: To sign with" # must be in keychain
# unzip the ipa
unzip -q "$IPA"
# remove the signature
rm -rf Payload/*.app/_CodeSignature
# replace the provision
cp "$PROVISION" Payload/*.app/embedded.mobileprovision
# sign with the new certificate (--resource-rules has been deprecated OS X Yosemite (10.10), it can safely be removed)
/usr/bin/codesign -f -s "$CERTIFICATE" --resource-rules Payload/*.app/ResourceRules.plist Payload/*.app
# zip it back up
zip -qr resigned.ipa Payload
```

Your new signed app is called resigned.ipa

[GitSourceHub](https://stackoverflow.com/questions/5160863/how-to-re-sign-the-ipa-file/16426800)

