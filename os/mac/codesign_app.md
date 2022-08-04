# Code sign App


## Manual Sign

Apple removed app's certificate, so the app will crash. The current solution is to sign it yourself.

Run in Terminal

> codesign --force --deep --sign - /Applications/name.app

You could use 'sudo' for escalated permissions.