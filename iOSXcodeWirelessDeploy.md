# Xcode iOS Xcode Wireless Deploy

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

#### Wireless Deploy Devices list

![alt text][image]

[image]: iOSiPAAssets/wirelessDeployDevicesBefore.png "Wireless Deploy Devices list Kautilya"

#### You could download the project via this link [Dicey App Source Code](https://github.com/SensehacK/Dicey)

### Step 2

Check the Devices list wherein it would display all of the devices & simulators available to run.provisioning profiles or certificates.
When your iOS device gets displayed you can select **Window** -> **Devices and Simulators** which will make a display a new pop up window.

#### Wireless Deploy Location

![alt text][image]

[image]: iOSiPAAssets/wirelessDeployMenuOption.png "Wireless Deploy Menu Kautilya"

### Step 3

Select **iOS Device** in select device screen. Check the **Connect via Network** option.
That's it, no more messing with wires, unless you want to charge your iOS devices which doesn't support wireless charging.

#### App Devices Window

![alt text][image]

[image]: iOSiPAAssets/wirelessDeployDevicesWindow.png "Wireless Deploy Window Kautilya"

### Step 4

Disconnect the iOS device via cable and now in Xcode device selection screen, it would display an icon of network besides the device name.

Note: For wireless deployment to work, both the workstation and iOS device should be connected on the same network through Wireless router or Mobile Hotspot.

#### Devices list Success

![alt text][image]

[image]: iOSiPAAssets/wirelessDeployDevicesSuccess.png "Wireless Deploy Devices Success Kautilya"

### Step 5

## Profit ???

:grin:

## Author : [Kautilya Save](https://kautilya.design/)

### [GitHub](https://github.com/SensehacK)