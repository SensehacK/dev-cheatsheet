# Sonarr

## Intro

## Guide

Good Guides for following  `Sonarr`
[https://trash-guides.info/](https://trash-guides.info/Sonarr/)

## Background ARM32

Context regarding Raspberry PI 

A year ago, around 2/3 of our Arm users were still on 32-bit platforms, today it's less than 1/5, and consequently we have taken the difficult decision to formally deprecate 32-bit Arm builds from 2023-07-01. Due to the number of images and how our build pipelines work there's going to be some wiggle room here, but essentially from the 1st of July 2023 we will no longer support any 32-bit platforms.

Old images will continue to work, but will not receive application or OS updates, and we will not provide support for them. Additionally, the `latest` and `arm32v7-latest` tags will no longer work for 32-bit Arm, you will need to provide a specific version tag if you wish to pull one of the old images.

If you're currently using our 32-bit Arm images, what are your options?

- If you're not sure what architecture you're on, run `uname -m` from a terminal session - a response of `armv7l` or `armhf` means you're running a 32-bit kernel.
- You may also have a 64-bit kernel with a 32-bit userspace, especially if you're running an OS like LibreELEC or OSMC, which likely means a 32-bit Docker install. Running `getconf LONG_BIT` will give you a response of `32` if this is the case.
- If your hardware is Armv8 and offers support for 64-bit, such as the Pi 3 or 4, or Zero 2 W, then look to migrate to a 64-bit OS.
- If your hardware is Armv7 or Armv6 you don't have a lot of options other than replacing it or accepting the risk and inconvenience of remaining on old versions of the images, the hardware simply doesn't support 64-bit.

As before, we know this probably isn't what you want to hear, but unfortunately technology marches forward and 32-bit is doomed. Hopefully by providing as much notice as possible you'll have time to find a solution that works for you.

https://www.linuxserver.io/blog/a-farewell-to-arm-hf

## ARM 32 Woes

Pi4 is 64 bit but the os runs in 32-bit userspace.

i found out that my pi4 is 32bit-arm so the inuxserver/sonarr:lastest image doesn't support. The last i support is linuxserver/sonarr:3.0.8.1507-ls151


sonarr
|Linuxserver.io version:- 3.0.8.1507-ls151|

[arm32v7-latest](https://hub.docker.com/layers/linuxserver/sonarr/arm32v7-latest/images/sha256-a2897fbe84b63965bba30a1f8b7341f4b63e6ef20862dfdd316e2a8dd4365627?context=explore)

image: linuxserver/sonarr:arm32v7-3.0.9

[arm32v7-3.0.9](https://hub.docker.com/layers/linuxserver/sonarr/arm32v7-3.0.9/images/sha256-2f56f6445567cc5833f669fc071fbc923b7434ab967e6e219164a6ef3b052562?context=explore)

docker: no matching manifest for linux/arm/v8 in the manifest list entries.
[Docker Jackett](https://github.com/ahuh/docker-arm-jackett)

[no arm32 version discussion reddit](https://www.reddit.com/r/sonarr/comments/wh0biw/comment/ijqngnj/?utm_source=share&utm_medium=mweb3x&utm_name=mweb3xcss&utm_term=1&utm_content=share_button)

###  This has problems starting up on Raspberry Pi v4 (64bit ARMv8) but docker / portainer space is 32Bit is my understanding

`image: linuxserver/jackett:arm64v8-latest`

This below has `curl -vvv https://1337x.to/` SSL 443 connection refuse error for trackers

`image: ahuh/arm-jackett`

This works fine with index / trackers
image: linuxserver/jackett:arm32v7-version-v0.20.754
Source [dockerhub](https://hub.docker.com/r/linuxserver/jackett)




