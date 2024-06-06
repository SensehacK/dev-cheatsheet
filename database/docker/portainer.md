# Portainer

## Intro


## Guide

Installing Portainer on Raspberry Pi
https://pimylifeup.com/raspberry-pi-portainer/

Downloading portainer from docker
```sh
sudo docker pull portainer/portainer-ce:latest
```
Running portainer from docker CLI.
```sh
sudo docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```




## Usage 

Used Portainer for managing docker images.

Issue while running Docker compose got solved by turning off Open VPN service in the background while Docker compose was executing some commands.


[SO](https://stackoverflow.com/questions/43720339/docker-error-could-not-find-an-available-non-overlapping-ipv4-address-pool-am)

Linux Media Server Script from this github also helped a lot.
[Github](https://github.com/GreenFrogSB/LMDS)

Solve a Limited Stack in Portainer
https://www.benjaminrancourt.ca/how-to-solve-a-limited-stack-in-portainer/

## Editing Configs

For some reason I couldn't use `vim` or `nano` but when I used `vi` it worked fine

https://github.com/portainer/portainer/issues/322#issuecomment-392251221

Or you can set environment files for docker containers or compose files

```sh
RUN apt-get update && apt-get install -y locales locales-all  
ENV LC_ALL en_US.UTF-8
```

## Commands




Restarting service
```sh
sudo docker restart portainer
```


[docker-error-could-not-find-an-available-non-overlapping-ipv4-address-pool-am](https://stackoverflow.com/questions/43720339/docker-error-could-not-find-an-available-non-overlapping-ipv4-address-pool-am)



## Watchtower

Updating Docker containers
https://github.com/containrrr/watchtower



## Error 


### `stack.env: no such file or directory`

https://github.com/portainer/portainer/issues/6701

### Solve a Limited Stack in Portainer

https://www.benjaminrancourt.ca/how-to-solve-a-limited-stack-in-portainer/

### Portainer Docker permission error

https://phoenixnap.com/kb/docker-permission-denied

### portainer not reachable 

500 internal error code
use this command

```sh
sudo systemctl restart docker
```






### mounting drives name conflict

Folder creation by Portainer - docker folders. 
So sometimes when restarted it creates a race condition to map a folder / directory for NAS / external HDD on Raspberry Pi. So I have to disable Portainer - containers like `transmission, radarr, sonarr`. and make sure that previous folder / directory gets named to something suffix_12 and then after restart the Raspberry Pi assigns the appropriate HDD name in `/media/pi/HDD_name`
Sometimes 



### deployment error - request failed with status code 500

This could be because of port being bind previously and some process still has a lock.

So we just restart our docker process by ssh the server.

```sh
sudo service docker stop
sudo service docker stop
```

[SO | relevant thread](https://stackoverflow.com/a/65559403)



## Reference

Linux Media Server Script from this [Github](https://github.com/GreenFrogSB/LMDS) also helped a lot.
