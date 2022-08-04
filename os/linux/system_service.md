System Control service


## Usage

Enabling a service or restarting a service can be done using `systemctl` command

> sudo systemctl SERVICE_NAME start

> sudo systemctl SERVICE_NAME stop

> sudo systemctl SERVICE_NAME status

> sudo systemctl SERVICE_NAME restart

[Linux services](https://phoenixnap.com/kb/start-stop-restart-linux-services)


## Service on Boot

Enable auto run on system boot.

> sudo systemctl enable SERVICE_NAME


[Restart a service after crash](https://www.digitalocean.com/community/tutorials/how-to-configure-a-linux-service-to-start-automatically-after-a-crash-or-reboot-part-1-practical-examples)

[Periodic restart service](https://www.baeldung.com/linux/systemd-service-periodic-restart)