# Pi Hole

## Installation

I’m using ubuntu as my base machine to install PiHole on old pc hardware with Wifi card enabled.

## Config

web ui: [http://192.168.1.89/admin](http://192.168.1.89/admin)

DNS: [http://192.168.1.89](http://192.168.1.89)

Blocklist

Regex

https://pi-hole.net/
https://github.com/pi-hole/pi-hole

To install updates, run `pihole -up`
(https://docs.pi-hole.net/main/update/)


## Commands

https://docs.pi-hole.net/core/pihole-command/

https://discourse.pi-hole.net/t/the-pihole-command-with-examples/738

```sh
pihole status
pihole restartdns
```

Reboot Pi hole service

```sh
pihole restartdns

systemctl pihole-FTL restart
```



Reconfigure Pi Hole
You can run `pihole -r` and reconfigure the IP etc. That's probably the easiest.


## Rate limits

Changing the config to not rate limit my DNS resolution for clients connected.

Rate-limiting can easily be disabled by setting `RATE_LIMIT=0/0` in `/etc/pihole/pihole-FTL.conf`. If I want, say, to set a rate limit of 1 query per hour, the option should look like `RATE_LIMIT=1/3600`.

https://docs.pi-hole.net/ftldns/configfile/#rate_limit

https://www.reddit.com/r/pihole/comments/osm2fn/psa_if_you_are_having_random_dns_resolution/


## DNS 

`Maximum number of concurrent DNS queries reached`

Below list the following detailed steps that were taking to attempt to resolve this concern:

- Connect to pihole via SSH
    
- Navigate to /etc/dnsmasq.d/
    
- check to see if the following .conf exists on your Pihole instance  
    `02-custom-settings.conf`
    
- If this does not exist proceed with the following command  
    `sudo nano /etc/dnsmasq.d/02-custom-settings.conf`
    
- Add the following to the above .conf
    

```apache
#### EDIT SETTINGS
dns-forward-max=5096
min-cache-ttl=300
rebind-domain-ok=
#### END EDIT
```

- Save and exit the config
    
- Reboot your PiHole instance

[Source for above instructions](https://discourse.pi-hole.net/t/resolved-maximum-number-of-concurrent-dns-queries-reached/60970/2) 
