Xcode iOS iPA Package Generation.


Prerequisites: 

Xcode IDE
Mac OS 
iTunes
iOS Device



Creation: 

#Step 1:
Open your "Project_Name.xcproj" file from finder or Xcode recent items.
Select main project_name & in general check for any errors or warnings if any.

#Step 2: 
Check the App Bundle Identifier to match your Apple developer provisioning profiles or certificates.
If you select "Automatically manage signing" it is way easy for you.
If you select manual version do add the appropriate profiles & distribution certificates to the Apple Keychain.
Always choose allow for Keychain / Xcode as everytime you build apps to run on physical devices aside from simulator.
iOS requires you to run signed code, you cannot run unsign code unless you're bypassing the installation methods or have a jailbroken device.
