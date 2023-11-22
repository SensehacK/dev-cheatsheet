


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