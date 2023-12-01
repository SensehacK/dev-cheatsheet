## SMB Share

To share my external drive to be accessible on Windows Network drive as well as Google TV Chromecast OS.
Using Kodi with SMB is nice - no transcoding required for using subtitles for Anime or foreign languages.
Also plugging in Google TV Chromecast dongle into the Sync box for light strips to be synced is nice rather than turning on my PC to output that home theatre experience.


Restarting the SMB service 
```sh
sudo systemctl restart smbd
```

Editing the configuration file for SMB

```sh
sudo nano /etc/samba/smb.conf
```

Setting password for SMB user
```sh
sudo smbpasswd -a kautilya
```

[PiMyLifeUp](https://pimylifeup.com/raspberry-pi-samba/)

[SMB Setup RPi4](https://jamesdixon.dev/posts/setting-up-smb-on-a-raspberry-pi/)