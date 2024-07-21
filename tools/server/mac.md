
## MindMap

[vnc](vnc.md)


## Configure

macOS Remote access
[configure remote access | article](https://wcsng.ucsd.edu/docs/technical/remote_access/remote_access_macos/) 

## Debugging VNC

### Ping

First ping the host IP address to make sure you can access it.


```sh
PING 10.21.24.21
```

### SSH

Do ssh to the macOS server to check whether you can login properly.

[read more about logging in via ssh](ssh.md)

### Connection timeouts

```log
Timed out waiting for a response from the computer
```
I did restart of the VNC / ARD service as well to debug this issue.
No avail.
Tried to connect via public IP as well, didn't work.

### configure firewall

[How to Fix VNC Error: “Timed out waiting for the response from the host computer”](https://blog.racknerd.com/how-to-fix-vnc-error-timed-out-waiting-for-the-response-from-the-host-computer/)


### VNC Errors

[realVNC error messages](https://help.realvnc.com/hc/en-us/articles/360002254738-RealVNC-Connect-Error-Messages)

[known issues for macOS |  VNC](https://help.realvnc.com/hc/en-us/articles/360002712837-Known-Issues-when-connecting-to-macOS#device-access-0-0)

## Monitor 

### Clients

Monitor the remote connected clients to the server

```sh
# monitor via process name
netstat -a | grep vnc

# Monitor via Port address
netstat -na | grep '[:.]5900'
```

### Service

Status of VNC service

```sh
ps -e | grep ARDAgent
```

## Restart

### VNC Service

```sh
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart \
-activate -configure -access -on \
-clientopts -setvnclegacy -vnclegacy yes \
-clientopts -setvncpw -vncpw mypasswd \
-restart -agent -privs -all
```

Good github gist of enabling, restarting the macOS vnc server via CLI commands.

[github gist source](https://gist.github.com/nateware/3915757) 

### Mac

[apple support guide](https://support.apple.com/guide/terminal/restart-computers-apd7d247a89-3560-4c3b-a471-3e66ff607040/mac)

Shutdown command

```sh
sudo shutdown -r now
```

## Mount DMG

CLI
[How-to-install-dmg-and-dkg-on-mac-via-terminal](https://cyb.tw/docs/Tech/2021/3/17_How-to-install-dmg-and-dkg-on-mac-via-terminal.html)

[SE | is-there-a-command-to-install-a-dmg](https://apple.stackexchange.com/questions/73926/is-there-a-command-to-install-a-dmg)



## Force quit

Press these three keys together: Option (or Alt), Command, Esc (Escape). Or **choose Force Quit from the Apple menu  in the corner of your screen**. The Finder is always open, but if it stops responding, you can force it to quit and then open again: Select Finder in the Force Quit window, then click Relaunch

## Disable iBoss Proxy


```sh
cd /Applications/Utilities/iboss.app/gen4agent/
# disable
./reconfigure.sh unload

# enable
./reconfigure.sh load
```


## Retrieve Serial number

```sh
system_profiler SPHardwareDataType | awk '/Serial/ {print $4}'
```
[Stack exchange post](https://apple.stackexchange.com/a/40244)


## disable sleep

X would be the seconds

```sh
caffeinate -t X 

# Does it infinitly
caffeinate -d
```

Also could set the power management to disable sleep using Command Line

Use 0 to reenable sleep.

```sh
sudo pmset disablesleep 1
```

Read more about [utilities wrapper around sleeping mac](tools/apps#dev%20utility)

Additionally, if you have an application full screen - the system should never sleep the display or go to screensaver. Have to test this out though!
Or you could plug in `hdmi dummy` to keep the GPU or mac alive | consumes more power though.
