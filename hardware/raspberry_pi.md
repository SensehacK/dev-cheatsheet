# Raspberry PI


## OS Versions

You can use from plethora of options for better support.

I wanted to try `Diet Pi` but went with Raspbian Pi - Debian based RPi 4 image officially recommended.

**Run to confirm**. 
```sh
uname -m
```

If it says `aarch64` then it is 64 bit. If it says `armv7l` then it is 32 bit.

## Pi Hole

Used basic installation steps for network local DNS blocker on my local network.

[pi_hole](pi_hole.md)

## Root

File manager GUI with root privileges use this command.

Open the Terminal
```sh
sudo pcmanfm
```

## Plex Media Server


Restart service 

```sh
sudo service plexmediaserver restart
```

You can use `start` or `stop`

Check status

```sh
sudo service plexmediaserver status
```

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


## HDD name conflict

Folder creation by Portainer - docker folders. 
So sometimes when restarted it creates a race condition to map a folder / directory for NAS / external HDD on Raspberry Pi. So I have to disable Portainer - containers like `transmission, radarr, sonarr`. and make sure that previous folder / directory gets named to something suffix_12 and then after restart the Raspberry Pi assigns the appropriate HDD name in `/media/pi/HDD_name`
Sometimes 

## Open VPN

```sh
sudo service openvpn start
sudo service openvpn stop
```

## Docker

Used Portainer for managing docker images.

Issue while running Docker compose got solved by turning off Open VPN service in the background while Docker compose was executing some commands.

### Portainer

Downloading portainer from docker
```sh
sudo docker pull portainer/portainer-ce:latest
```
Running portainer from docker CLI.
```sh
sudo docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

Restarting service
```sh
sudo docker restart portainer
```

https://pimylifeup.com/raspberry-pi-portainer/

[SO](https://stackoverflow.com/questions/43720339/docker-error-could-not-find-an-available-non-overlapping-ipv4-address-pool-am)

Linux Media Server Script from this github also helped a lot.
[Github](https://github.com/GreenFrogSB/LMDS)

Solve a Limited Stack in Portainer
https://www.benjaminrancourt.ca/how-to-solve-a-limited-stack-in-portainer/

Portainer Docker permission error
https://phoenixnap.com/kb/docker-permission-denied

portainer not reachable 
500 internal error code
use this command
'''
sudo systemctl restart docker





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

## Network


All your network settings are located in `etc/dhcpcd.conf`
Make sure if you want to edit the Ethernet interface or WLAN interface for Wireless.

```config
interface eth0
static ip_address=10.1.1.30/24
static routers=10.1.1.1
static domain_name_servers=10.1.1.1
```

https://raspberrypi.stackexchange.com/questions/37920/how-do-i-set-up-networking-wifi-static-ip-address-on-raspbian-raspberry-pi-os/74428#74428

https://raspberrypi.stackexchange.com/questions/110950/no-internet-via-ethernet-local-network-working

https://www.reddit.com/r/raspberry_pi/comments/117eizu/raspberry_pi_4_connects_to_wlan0_but_refuses_to/

FileZilla for connecting the FTP / SFTP server

https://stackoverflow.com/questions/12687900/connection-attempt-failed-with-econnrefused-connection-refused-by-server


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



## Internet Down


So my raspberry pi internet was down partly because I have manually configured my nameserver in conf file.
Location : /etc/resolv.conf


```config
# Generated by resolvconf
nameserver 192.168.0.1
nameserver 8.8.8.8
nameserver 192.168.0.88
nameserver 208.67.222.222
```


Below is the post copied from [Reddit comment](https://www.reddit.com/r/raspberry_pi/comments/117eizu/raspberry_pi_4_connects_to_wlan0_but_refuses_to/) 
Since you never know which subreddit or internet goes offline, deleted post etc.


A standard trick to differentiate between a low-level network problem and a DNS issue is to ping 8.8.8.8 which is google’s DNS server.

- If you can ping 8.8.8.8 successfully, then your network is good but your DNS is hosed. Look at /etc/resolv.conf and check the name server setting.
    
- If you can’t ping google DNS, then try pinging your router. This is often 192.168.0.1 but check another computer connected to the same router for the correct address.
    
    - also run ‘ip a’ or ‘ifconfig’ to check the IP address assigned to wlan0
        
- if you can’t ping your router, you probably have a Wi-Fi issue, or perhaps a DHCP server issue with your router (power cycling your router can sometimes solve).
    

Post back what you find out



## Raspberry PI ARM Architecture 


A year ago, around 2/3 of our Arm users were still on 32-bit platforms, today it's less than 1/5, and consequently we have taken the difficult decision to formally deprecate 32-bit Arm builds from 2023-07-01. Due to the number of images and how our build pipelines work there's going to be some wiggle room here, but essentially from the 1st of July 2023 we will no longer support any 32-bit platforms.

Old images will continue to work, but will not receive application or OS updates, and we will not provide support for them. Additionally, the `latest` and `arm32v7-latest` tags will no longer work for 32-bit Arm, you will need to provide a specific version tag if you wish to pull one of the old images.

If you're currently using our 32-bit Arm images, what are your options?

- If you're not sure what architecture you're on, run `uname -m` from a terminal session - a response of `armv7l` or `armhf` means you're running a 32-bit kernel.
- You may also have a 64-bit kernel with a 32-bit userspace, especially if you're running an OS like LibreELEC or OSMC, which likely means a 32-bit Docker install. Running `getconf LONG_BIT` will give you a response of `32` if this is the case.
- If your hardware is Armv8 and offers support for 64-bit, such as the Pi 3 or 4, or Zero 2 W, then look to migrate to a 64-bit OS.
- If your hardware is Armv7 or Armv6 you don't have a lot of options other than replacing it or accepting the risk and inconvenience of remaining on old versions of the images, the hardware simply doesn't support 64-bit.

As before, we know this probably isn't what you want to hear, but unfortunately technology marches forward and 32-bit is doomed. Hopefully by providing as much notice as possible you'll have time to find a solution that works for you.

https://www.linuxserver.io/blog/a-farewell-to-arm-hf


## Sonarr Radarr Jackett arch ARM 32 / v7 woes


Pi4 is 64 bit but the os runs in 32-bit userspace.

i found out that my pi4 is 32bit-arm so the inuxserver/sonarr:lastest image doesn't support. The last i support is linuxserver/sonarr:3.0.8.1507-ls151

https://github.com/linuxserver/docker-radarr/tree/3.0.2.4552-ls102

Radarr
|Linuxserver.io version:- 3.0.2.4552-ls102|

Latest: [arm32v7-4.5.2](https://hub.docker.com/layers/linuxserver/radarr/arm32v7-4.5.2/images/sha256-a6a697eb9a1c0edaf8b5a966e320135bf730707322ff5f4c54bafe7e193a9bad?context=explore)

https://hub.docker.com/r/linuxserver/radarr/tags?page=1&name=arm32

sonarr
|Linuxserver.io version:- 3.0.8.1507-ls151|

[arm32v7-latest](https://hub.docker.com/layers/linuxserver/sonarr/arm32v7-latest/images/sha256-a2897fbe84b63965bba30a1f8b7341f4b63e6ef20862dfdd316e2a8dd4365627?context=explore)

image: linuxserver/sonarr:arm32v7-3.0.9

[arm32v7-3.0.9](https://hub.docker.com/layers/linuxserver/sonarr/arm32v7-3.0.9/images/sha256-2f56f6445567cc5833f669fc071fbc923b7434ab967e6e219164a6ef3b052562?context=explore)

docker: no matching manifest for linux/arm/v8 in the manifest list entries.
Docker Jackett
https://github.com/ahuh/docker-arm-jackett

https://www.reddit.com/r/sonarr/comments/wh0biw/comment/ijqngnj/?utm_source=share&utm_medium=mweb3x&utm_name=mweb3xcss&utm_term=1&utm_content=share_button


# This has problems starting up on Raspberry Pi v4 (64bit ARMv8) but docker / portainer space is 32Bit is my understanding.

`image: linuxserver/jackett:arm64v8-latest`

This below has `curl -vvv https://1337x.to/` SSL 443 connection refuse error for trackers

`image: ahuh/arm-jackett`

This works fine with index / trackers
image: linuxserver/jackett:arm32v7-version-v0.20.754
https://hub.docker.com/layers/linuxserver/jackett/arm32v7-version-v0.20.754/images/sha256-64c2e0954cb65213e5a1a172228f69c24e307967aa5184cf7ea1ad86326f7078


