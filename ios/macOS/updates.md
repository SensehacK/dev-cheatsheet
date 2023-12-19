

## Intro

## Installer 

```sh
softwareupdate --fetch-full-installer --full-installer-version 13.0.1
```

## Companion app

[Mist Xcode companion apps](https://github.com/ninxsoft/Mist)

[App to create configuration profile](https://github.com/ProfileCreator/ProfileCreator)

Convert macOS [property lists into configuration profiles](https://github.com/timsutton/mcxToProfile)

[Apple Configurator](https://support.apple.com/apple-configurator)

[iMazing profile editor](https://imazing.com/profile-editor)

## Downgrading Avoiding updates

You can avoid updates for your mac by adding the update server to your host file to return empty response so macOS won't be able to ping the update servers.

## MDM

Or you can go for having MDM profile installed which limits your macOS to not upgrade to a specific OS or stay within the range of specific versions in the allowlist.

Apple doc around [MDM restrictions](https://support.apple.com/guide/deployment/restrictions-for-mac-depba790e53/web)
How to setup using [apple configurator support article](https://support.apple.com/pl-pl/guide/apple-configurator-2/pmd85719196/mac)

Deploying your MDM profiles using MicroMDM [quick start guide](https://github.com/micromdm/micromdm/blob/master/docs/user-guide/quickstart.md)

### Removing MDM Profiles

[delete mdm profile on mac](https://www.imobie.com/iphone-unlocker/how-to-delete-an-mdm-profile-on-mac.htm)

## Internal Links

Read more about iOS or other non macOS [MDM here](mdm.md)

Internal documentation about [software_updates](software_updates.md)

## Link

[apple support article around macOS updates](https://support.apple.com/en-us/102662)

[how-to-download-macos-catalina-mojave-or-high-sierra-full-installers/](https://mrmacintosh.com/how-to-download-macos-catalina-mojave-or-high-sierra-full-installers/)
