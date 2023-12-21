


## Compose


Sending specific commands in docker compose
```yaml
version: "2.11"
services:
    # Disables ipv6  
    sysctls:
        - net.ipv6.conf.all.disable_ipv6=1
```

https://stackoverflow.com/questions/39329732/specify-sysctl-values-using-docker-compose


## Errors
### ModuleNotFoundError: No module named 'websocket' at `up` command

Seems a `sudo pip` issue. In facts,
```sh
sudo pip install jsonschema websocket
```

[Github Issue](https://github.com/docker/compose/issues/8574#top)


## Dependency Startup order

[startup order](https://docs.docker.com/compose/startup-order/)

[depends_on](https://docs.docker.com/compose/compose-file/05-services/#depends_on)


```bash
[Service]
ExecStartPre=/bin/sleep 30
```

[Delayed starting of Docker service until expected mounts are available](https://davejansen.com/systemctl-delay-start-docker-service-until-mounts-available/)

