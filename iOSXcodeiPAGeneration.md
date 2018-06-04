# Xcode iOS iPA Package Generation.


## Prerequisites: 

* Xcode IDE
* Mac OS 
* iTunes
* iOS Device



## Creation: 

### Step 1:
Open your "Project_Name.xcodeproj" file from finder or Xcode recent items.
Select main project_name & in general check for any errors or warnings if any.

### Step 2: 
Check the App Bundle Identifier to match your Apple developer provisioning profiles or certificates.
If you select "Automatically manage signing" it is way easy for you.
Reference Image: 
![alt text][image]

[image]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/automatic_Signing.png "Automatic Signing Kautilya"


If you select manual version do add the appropriate profiles & distribution certificates to the Apple Keychain.
Always choose allow for Keychain / Xcode as everytime you build apps to run on physical devices aside from simulator.
Reference Image: 
![alt text][image2]

[image2]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/manual_Signing.png "Manual Signing Kautilya"

iOS requires you to run signed code, you cannot run unsign code unless you're bypassing the installation methods or have a jailbroken device.


### Step 3: 
Select "Generic iOS Device" in select device screen.
Reference Image: 
![alt text][image3]

[image3]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/select_Generic_iOS_Device.png "select_Generic_iOS_Device Kautilya"

After you have selected your Xcode should show up like this.


Reference Image: 
![alt text][image4]

[image4]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/selected_generic_device.png "selected generic device Kautilya"


Archiving Button & progress 
Reference Image: 
![alt text][image5]

[image5]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/product_archive.png "selected generic device Kautilya"

Reference Image: 
![alt text][image6]

[image6]: https://github.com/SensehacK/iOSDocumentation/blob/master/iOSiPAAssets/archive_progress.png "selected generic device Kautilya"




### Step 4: 

### Step 5: 