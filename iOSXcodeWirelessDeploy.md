# Xcode iOS iPA Package Generation

When we are working with Xcode for app development we usually tether our iOS devices to the Mac for deploying apps but Xcode 9 introduces Wireless Deployment - Debugging and this 5 minute guide will help you in setting that up. Switch to wireless.

## Prerequisites

* Xcode 9+ IDE
* Mac OS
* Wireless Network
* iOS 10+ Device

## Creation

### Step 1

Open your **Project_Name.xcodeproj** file from finder or Xcode recent items.
Select main project_name & in general check for any errors or warnings if any.
Connect iPhone or iPad to the Mac & press Trust this computer.

### Step 2

Check the Devices list wherein it would display all of the devices & simulators available to run.provisioning profiles or certificates.
When your iOS device gets displayed you can select **Window** -> **Devices and Simulators** which will make a display a new pop up window.

#### Automatic Signing

![alt text][image]

[image]: iOSiPAAssets/automatic_Signing.png "Automatic Signing Kautilya"

#### You could download the project via this link [Dicey App Source Code](https://github.com/SensehacK/Dicey)

If you select manual version do add the appropriate profiles & distribution certificates to the Apple **Keychain**.
Always choose allow for Keychain / Xcode as every time you build apps to run on physical devices aside from simulator.

### Step 3

Select **iOS Device** in select device screen. Check the **Connect via Network** option.
That's it, no more messing with wires, switch to wireless.

#### Select Generic iOS Device

![alt text][image3]

[image3]: iOSiPAAssets/select_Generic_iOS_Device.png "select_Generic_iOS_Device Kautilya"

After you have selected your Xcode should show up like this.

#### Selected generic device

![alt text][image4]

[image4]: iOSiPAAssets/selected_generic_device.png "selected generic device Kautilya"

Archiving Button & progress

### Step 4

Disconnect the iOS device via cable and now in Xcode device selection screen, it would display an icon of network besides the device name.

Note: For wireless deployment to work, both the workstation and iOS device should be connected on the same network through Wireless router or Mobile Hotspot.

### Step 5

## Profit ???

:grin:

## Author : [Kautilya Save](https://kautilya.design/)

### [GitHub](https://github.com/SensehacK)