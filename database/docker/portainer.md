# Portainer


Used Portainer for managing docker images.

Issue while running Docker compose got solved by turning off Open VPN service in the background while Docker compose was executing some commands.

Installing Portainer on Raspberry Pi
https://pimylifeup.com/raspberry-pi-portainer/

[SO](https://stackoverflow.com/questions/43720339/docker-error-could-not-find-an-available-non-overlapping-ipv4-address-pool-am)

Linux Media Server Script from this github also helped a lot.
[Github](https://github.com/GreenFrogSB/LMDS)

Solve a Limited Stack in Portainer
https://www.benjaminrancourt.ca/how-to-solve-a-limited-stack-in-portainer/


### Error 


`stack.env: no such file or directory`
https://github.com/portainer/portainer/issues/6701


## Watchtower

Updating Docker containers
https://github.com/containrrr/watchtower

## Editing Configs

For some reason I couldn't use `vim` or `nano` but when I used `vi` it worked fine

https://github.com/portainer/portainer/issues/322#issuecomment-392251221

Or you can set environment files for docker containers or compose files

```sh
RUN apt-get update && apt-get install -y locales locales-all  
ENV LC_ALL en_US.UTF-8
```
