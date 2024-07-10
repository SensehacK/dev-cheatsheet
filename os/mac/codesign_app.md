# Code sign App


## Manual Sign

Apple removed app's certificate, so the app will crash. The current solution is to sign it yourself.

Run in Terminal

```sh
codesign --force --deep --sign - /Applications/name.app

```
You could use 'sudo' for escalated permissions.


## Cannot Open the program

If the error “Cannot open the program” appears, enter in the terminal (the application should be in the “Programs” folder):

```sh
xattr -cr /Applications/AppName.app && codesign --force --deep --sign - /Applications/AppName.app
```

The update has been completed. Please uninstall and reinstall completely.