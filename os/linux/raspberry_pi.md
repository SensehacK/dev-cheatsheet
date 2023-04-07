# Raspberry PI


## OS Versions

You can use from plethora of options for better support.

I wanted to try `Diet Pi` but went with Raspbian Pi - Debian based RPi 4 image officially recommended.

## Pi Hole

Used basic installation steps for network local DNS blocker on my local network.

[pi_hole](pi_hole.md)

## Root

File manager GUI with root privileges use this command.

Open the Terminal
> sudo pcmanfm

`


## Plex Media Server


Restart service 

> sudo service plexmediaserver restart

You can use `start` or `stop`

Check status

> sudo service plexmediaserver status

Update plex on Debian

```bash
sudo apt list --upgradable plexmediaserver
```


```bash
sudo apt upgrade plexmediaserver -y
```

https://ownyourstreaming.com/server/update-plex-on-rpi

### Permission Plex Users Groups

Error while accessing mounted external disk by plex user.

[Ask Ubuntu](https://askubuntu.com/questions/150909/plex-wont-enter-my-home-directory-or-other-partitions)

(https://smyl.es/how-to-move-plex-metadata-and-index-data-to-new-driver-andor-directory-location/?doing_wp_cron=1646545387.6087911128997802734375)

### Other Tools for Plex

Tautolli

Ombi

## JellyFin

Restarting Jellyfin
 
```bash
sudo service jellyfin restart
``` 

https://pimylifeup.com/raspberry-pi-jellyfin/


## SMB Share

To share my external drive to be accessible on Windows Network drive as well as Google TV Chromecast OS.
Using Kodi with SMB is nice - no transcoding required for using subtitles for Anime or foreign languages.
Also plugging in Google TV Chromecast dongle into the Sync box for light strips to be synced is nice rather than turning on my PC to output that home theatre experience.


Restarting the SMB service 

> sudo systemctl restart smbd

Editing the configuration file for SMB

> sudo nano /etc/samba/smb.conf

Setting password for SMB user

> sudo smbpasswd -a kautilya


[PiMyLifeUp](https://pimylifeup.com/raspberry-pi-samba/)

[SMB Setup RPi4](https://jamesdixon.dev/posts/setting-up-smb-on-a-raspberry-pi/)

## Mount Drives

It auto mounted my external HDD on the media or mount folder. I don't recall what steps I took in order to make it workable to link the HDD to my Pi.



## Open VPN


> sudo service openvpn start

> sudo service openvpn stop

## Docker

Used Portainer for managing docker images.

Issue while running Docker compose got solved by turning off Open VPN service in the background while Docker compose was executing some commands.

[SO](https://stackoverflow.com/questions/43720339/docker-error-could-not-find-an-available-non-overlapping-ipv4-address-pool-am)

Linux Media Server Script from this github also helped a lot.
[Github](https://github.com/GreenFrogSB/LMDS)

Solve a Limited Stack in Portainer
https://www.benjaminrancourt.ca/how-to-solve-a-limited-stack-in-portainer/


## Kill Switch

## Storage

If your raspberry Pi always becomes full with storage you could try few of these things


This deletes the old cache package files on the system. Could help you regain approx 200-500MB of storage.

> sudo apt-get clean


This command lists all of the mounted drives on the system. You can further investigate on how each folder takes space.
> df -h 

Further storage drill down

> du -sh /*

https://forums.raspberrypi.com/viewtopic.php?t=15908




## Root File Manager

> sudo pcmanfm

[File manager with root privileges](https://forums.raspberrypi.com/viewtopic.php?t=164083)
## Related Links

My Favorite tutorials overall.
[Raspberry Pi Playlist](https://www.youtube.com/playlist?list=PLYl5sY0sL98hJRpne6ShX1I9JJ6MVIH4q)

[Pi Plex Server](https://www.youtube.com/watch?v=Hgy_YOQBdTw&list=PLYl5sY0sL98hJRpne6ShX1I9JJ6MVIH4q&index=36&t=637s)
[HOW TO INSTALL SONARR DOCKER ON A RASPBERRY PI 4](https://www.youtube.com/watch?v=xW0hbxeef6c)


## Users

VCHI Initialization failed

https://raspberrypi.stackexchange.com/questions/7546/munin-node-plugins-vchi-initialization-failed


## Migration SD Card to SSD

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



## RetroPie


Bootable from SSD
Argon M2 SSD case Raspberry Pi 4


Controllers Bluetooth pairing
Configuration -> Bluetooth.

File ROM transfers


Wifi setup

https://retropie.org.uk/docs/Wifi/


4K Lag issue
Flag to set it to 1080P

https://retropie.org.uk/docs/Pi4/?h=config.txt#issues-using-a-4k-tv