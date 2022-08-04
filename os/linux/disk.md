Disk

## List



## Mount

For mounting the disk you have to mount it via command line.
NTFS package may be necessary to install for supporting Windows based HDD format.



## Deleting Cache

My Raspberry Pi had 100% storage in `/dev/root/` 
Running this command saved me some space

> sudo apt-get clean

[Stack Exchange](https://raspberrypi.stackexchange.com/questions/58979/root-filesystem-usage-at-100-but-i-cant-see-why)

Believe so my Docker images are taking too much space.





## Storage Details

Using the command below you can see the storage usage of your linux systems.

>  df -h


## SMB 

To check the service status

> sudo service smbd status


To turn on / restart smbd service

> sudo systemctl restart smbd