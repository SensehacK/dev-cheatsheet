

## NTFS


Mounting NTFS 

Utilizing app called [Mounty](https://www.mounty.app/)

```sh
brew install --cask macfuse
brew install gromgit/fuse/ntfs-3g-mac
brew install --cask mounty
```

Had to enable / disable system extensions for macOS.


## Storage


You can check why your macOS is low on storage.

Few good links about macOS caching about everything in its system directory.
One single Xcode installation can go up to 60gigs of storage. This is pretty bad for apple hardware where Memory costs like Caviar be it Volatile (RAM, L1.*x Cache) or Non Volatile (Disk / SSD / ROM).

Luckily apple provides us two options

- One is there System Preferences -> Storage with some option to delete unused storage and cleanup extra support libraries.
- It tries to upsell iCloud Storage packages to offload mac / device storage to Cloud. Seamless integration or anti competitive - forced planned obsolescence type of stuff. You can be the judge.


I recommend few things

- [Daisy disk](https://daisydiskapp.com/)
- [Clean my Mac](os/mac/disk_utility#Clean%20my%20Mac) 
- Terminal commands 
- Disable Time Machine
- Delete old iOS / iPhone backups
- Enable [hidden_files](hidden_files.md)

### Support Files

Delete Phone old OS device support files, for example if you had an iOS / iPadOS / Apple TV / Vision Pro or any apple development device on a specific OS and then you upgraded from iOS 16.4 -> iOS 17.4 then Xcode or macOS has old iOS 16.4 device support files for Obj-C / Swift Headers or just for debugging symbols. That's why every time you connect a new device to xcode -> it performs this process of `Preparring for Device support`

Turns out if you have like 4 - 7 development devices for one Xcode the storage support files goes up to 20Gigs+ usually each device + OS combo accounting for 2 - 4 gigs.
You can delete them in `Apple -> System preferences app -> Developer -> Delete Device Support Files`


### Terminal Commands

`du` (disk usage) and `df` (disk free) commands


```sh
df -h | grep Gi

# Output
# /System/Volumes/Data 124Gigs 
```

This grabs space occupied by `Gigs` and then you can sort that data

```sh
du -h /System/Volumes/Data | grep "G\t" | sort
```

and if you want breakdown of the folders / directory use

```sh
du -h -d 1
```

### Clean my Mac

 [Clean my Mac - MacPaw](https://cleanmymac.com/)
 Just make sure to disable everything else like analytics, full disk scanning, protection stuff etc & auto login. I usually use this app once in 30 days. 
 