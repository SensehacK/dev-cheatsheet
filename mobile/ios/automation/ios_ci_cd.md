# Xcode iOS CICD

## Prerequisites

* Microsoft VSTS
* Xcode IDE
* Mac OS
* iOS Device
* Microsoft App Center
* Ftp server

## Creation

This article is just a template of iOS Xcode IPA generation, I haven’t really got time to sit down and document my process last time I had chance to deploy an iPA directly to ad-hoc organization. I would love to work on this cheatsheet again when I get Apple developer account which allows me to create provisioning profiles and sign iPAs for Ad-hoc distribution. Though I could maybe just utilize my freemium apple developer account, may need to deep dive on that one.

### Step 1

Open your **Project\_Name.xcodeproj** file from finder or Xcode recent items. Select main project\_name & in general check for any errors or warnings if any.

### Step 2

Check the App Bundle Identifier to match your Apple developer provisioning profiles or certificates. If you select "Automatically manage signing" it gets a bit easier or else the old way to signing each component respectively also works fine.

#### Automatic Signing

![Automatic Signing Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/automatic_Signing.png)

#### You could download the project via this link [Dicey App Source Code](https://github.com/SensehacK/Dicey)

If you select manual version do add the appropriate profiles & distribution certificates to the Apple **Keychain**. Always choose allow for Keychain / Xcode as every time you build apps to run on physical devices aside from simulator.

#### Manual Signing

![Manual Signing Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/manual_Signing.png)

iOS requires you to run signed code, you cannot run unsign code unless you're bypassing the installation methods or have a jailbroken device.

### Step 3

Select **Generic iOS Device** in select device screen.

#### Select Generic iOS Device

![select\_Generic\_iOS\_Device Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/select_Generic_iOS_Device.png)

After you have selected your Xcode should show up like this.

#### Selected generic device

![selected generic device Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/selected_generic_device.png)

Archiving Button & progress

#### Product archive

![product\_archive Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/product_archive.png)

#### Archive progress started

![archive\_progress Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/archive_progress.png)

#### Archive progress succeeded

![archive\_progress succeeded Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/archive_successful.png)

### Step 4

Use Xcode menu bar **Window** -&gt; **Organizer**

#### Window Organizer

![window\_organizer Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/window_organizer.png)

After that new window will pop up & then select export button at the right sidebar.

#### Export Organizer

![export\_organizer Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/export_organizer.png)

A new window will pop up & select the option **Development** & press **Next**.

#### Organizer Development

![organizer\_development Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/organizer_development.png)

Choose the following options as depicted in the screenshot & press **Next**.

#### Organizer Development Options

![organizer\_development\_options Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/organizer_development_options.png)

Choose the following options as depicted in the screenshot & press **Next**.

#### Organizer Development Certificate

![organizer\_development\_certificate Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/organizer_development_certificate.png)

### Step 5

Export from Xcode to Finder Choose the **Export** button from Organizer window.

#### Organizer iPA Success

![organizer\_ipa\_success Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/organizer_ipa_success.png)

Select the location for iPA export in finder & click **Export** button.

#### Export finder

![export\_finder Kautilya](https://github.com/SensehacK/dev-cheatsheet/tree/88f67add347b1607b94f5c5ac6ec7917192dddf6/iOS/Automation/iOSiPAAssets/export_finder.png)

Navigate to that folder & copy that iPA file to your desired application.

### Step 6

## Profit ??

:grin:

## Author : [Kautilya Save](https://kautilya.design/)

### [GitHub](https://github.com/SensehacK)

