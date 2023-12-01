# Raspberry PI

## [System Info](system_info.md)

## [Pi Hole](pi_hole.md)

Used basic installation steps for network local DNS blocker on my local network.



## [plex_media_server](plex_media_server.md)

## [jellyfin](jellyfin.md)

## [Docker](README_docker.md)

Used Portainer for managing docker images.

Issue while running Docker compose got solved by turning off Open VPN service in the background while Docker compose was executing some commands.
### [Portainer](portainer.md)



## [RetroPie](retro_pie.md)

## [radarr](radarr.md)

## [sonarr](sonarr.md)


## Storage

If your raspberry Pi always becomes full with storage you could try few of these things


This deletes the old cache package files on the system. Could help you regain approx 200-500MB of storage.

> sudo apt-get clean


This command lists all of the mounted drives on the system. You can further investigate on how each folder takes space.
> df -h 

Further storage drill down

> du -sh /*

https://forums.raspberrypi.com/viewtopic.php?t=15908


### Mount Drives

It auto mounted my external HDD on the media or mount folder. I don't recall what steps I took in order to make it workable to link the HDD to my Pi.


### [HDD name conflict](database/docker/portainer#mounting%20drives%20name%20conflict)

### Migration SD Card to SSD

`sudo rpi-eeprom-update -a`
`sudo reboot`

`sudo rpi-eeprom-config`

This boot order is exactly what we want. If the boot order code is anything other than BOOT_ORDER=0xf14, you can change the boot configuration using this command.  
`sudo -E rpi-eeprom-config --edit`

https://www.raspberrystreet.com/learn/how-to-boot-raspberrypi-from-usb-ssd

Backup raspberry pi images / SD card / OS 

https://raspberrystreet.com/learn/how-to-backup-raspberrypi-sdcard

USB boot order - Raspberry Pi
https://fossbytes.com/enable-usb-boot-on-raspberry-pi/

OS install guide
https://www.makeuseof.com/tag/install-operating-system-raspberry-pi/


https://raspberrytips.com/raspberry-pi-commands/





## [Open VPN](open_vpn.md)

[samba](samba.md)

## Related Links

My Favorite tutorials overall.
[Raspberry Pi Playlist](https://www.youtube.com/playlist?list=PLYl5sY0sL98hJRpne6ShX1I9JJ6MVIH4q)

[Pi Plex Server](https://www.youtube.com/watch?v=Hgy_YOQBdTw&list=PLYl5sY0sL98hJRpne6ShX1I9JJ6MVIH4q&index=36&t=637s)
[HOW TO INSTALL SONARR DOCKER ON A RASPBERRY PI 4](https://www.youtube.com/watch?v=xW0hbxeef6c)











