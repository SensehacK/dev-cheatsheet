# System Control service

## Usage

Enabling a service or restarting a service can be done using `systemctl` command

```sh
sudo systemctl SERVICE_NAME start
```

```sh
sudo systemctl SERVICE_NAME stop
```

```sh
sudo systemctl SERVICE_NAME status
```

```sh
sudo systemctl SERVICE_NAME restart
```

[Linux services](https://phoenixnap.com/kb/start-stop-restart-linux-services)

## Service on Boot

Enable auto run on system boot.

```sh
sudo systemctl enable SERVICE_NAME
```

[Restart a service after crash](https://www.digitalocean.com/community/tutorials/how-to-configure-a-linux-service-to-start-automatically-after-a-crash-or-reboot-part-1-practical-examples)

[Periodic restart service](https://www.baeldung.com/linux/systemd-service-periodic-restart)


## List services startup

To check all the services which are being run on startup / boot of unix / linux OS.

```sh
sudo service --status-all
```

For simple startup service management on Raspberry Pi I recommend tool rcconf. It allows you to easily turn on/off services in /etc/init.d/. You can also see if they are enabled and will run at startup.

To install the tool

```sh
sudo apt-get install rcconf
sudo rcconf
```

And is very simple to use it with text UI

[Super Use | How to tell which services run at startup](https://superuser.com/questions/852610/how-to-tell-which-services-run-at-startup-on-raspberry-pi-raspbian)

[How to Use systemd to Launch Programs at Startup on Raspberry Pi](https://www.makeuseof.com/what-is-systemd-launch-programs-raspberry-pi/)

## Delay

[How can I delay the startup of systemd services until the datetime is set (no RTC on the Raspberry Pi)](https://raspberrypi.stackexchange.com/questions/94635/how-can-i-delay-the-startup-of-systemd-services-until-the-datetime-is-set-no-rt)

Just found my preferred solution for this and commenting in case it helps someone else. do the "sudo systemctl edit docker.service" as described by [u/Parker_Hemphill](https://www.reddit.com/u/Parker_Hemphill/), but instead of the straight delay I added a dependency on a USB mount-point. Like the below. This way the service don't even start until the various (space-separated) paths are available first.

```config
[Unit]
#ExecStartPre=/bin/sleep 30
RequiresMountsFor=/media/localadmin/FILES /media/localadmin/PHOTOS
```

sleep 30 just left in there for my other's to see both options, but commented with the #

(Edit) changed service to unit