# Xcode iOS iPA Package Generation

## Prerequisites

* Xcode IDE
* Mac OS
* iTunes
* iOS Device

## Creation

### Step 1

Open your **Project_Name.xcodeproj** file from finder or Xcode recent items.
Select main project_name & in general check for any errors or warnings if any.

### Step 2

Check the App Bundle Identifier to match your Apple developer provisioning profiles or certificates.
If you select "Automatically manage signing" it is way easy for you.

#### Automatic Signing

![alt text][image]

[image]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/automatic_Signing.png "Automatic Signing Kautilya"

#### You could download the project via this link [Dicey App Source Code](https://github.com/SensehacK/Dicey)

If you select manual version do add the appropriate profiles & distribution certificates to the Apple **Keychain**.
Always choose allow for Keychain / Xcode as everytime you build apps to run on physical devices aside from simulator.

#### Manual Signing

![alt text][image2]

[image2]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/manual_Signing.png "Manual Signing Kautilya"

iOS requires you to run signed code, you cannot run unsign code unless you're bypassing the installation methods or have a jailbroken device.

### Step 3

Select **Generic iOS Device** in select device screen.

#### Select Generic iOS Device

![alt text][image3]

[image3]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/select_Generic_iOS_Device.png "select_Generic_iOS_Device Kautilya"

After you have selected your Xcode should show up like this.

#### Selected generic device

![alt text][image4]

[image4]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/selected_generic_device.png "selected generic device Kautilya"

Archiving Button & progress

#### Product archive

![alt text][image5]

[image5]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/product_archive.png "product_archive Kautilya"

#### Archive progress started

![alt text][image6]

[image6]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/archive_progress.png "archive_progress Kautilya"

#### Archive progress succeeded

![alt text][image7]

[image7]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/archive_successful.png "archive_progress succeeded Kautilya"

### Step 4

Use Xcode menu bar **Window** -> **Organizer**

#### Window Organizer

![alt text][image8]

[image8]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/window_organizer.png "window_organizer Kautilya"

After that new window will pop up & then select export button at the right sidebar.

#### Export Organizer

![alt text][image9]

[image9]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/export_organizer.png "export_organizer Kautilya"

A new window will pop up & select the option **Development** & press **Next**.

#### Organizer Development

![alt text][image10.a]

[image10.a]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/organizer_development.png "organizer_development Kautilya"

Choose the following options as depicted in the screenshot & press **Next**.

#### Organizer Development Options

![alt text][image10.b]

[image10.b]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/organizer_development_options.png "organizer_development_options Kautilya"

Choose the following options as depicted in the screenshot & press **Next**.

#### Organizer Development Certificate

![alt text][image11]

[image11]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/organizer_development_certificate.png "organizer_development_certificate Kautilya"

### Step 5

Export from Xcode to Finder
Choose the **Export** button from Organizer window.

#### Organizer iPA Success

![alt text][image12]

[image12]: iOSiPAAssets/organizer_ipa_success.png "organizer_ipa_success Kautilya"

Select the location for iPA export in finder & click **Export** button .

#### Export finder

![alt text][image13]

[image13]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/export_finder.png "export_finder Kautilya"

Navigate to that folder & copy that iPA file to your desired application.

### Step 6

## Profit ??

:grin:

## Author : Kautilya Save

### [GitHub](https://github.com/SensehacK)