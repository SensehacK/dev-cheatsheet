# automount volumes disable


> diskutil info /Volumes/Volume_name

Copy the Volume UDID

> sudo pico /etc/fstab

> UUID=Volume_UDID none volume_format(hfs,fat) rw,noauto 

[Cnet article](https://www.cnet.com/tech/computing/prevent-a-partition-from-mounting-in-os-x/)