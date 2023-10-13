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


## commands

https://discourse.pi-hole.net/t/the-pihole-command-with-examples/738


## Rate limits

Changing the config to not rate limit my DNS resolution for clients connected.

Rate-limiting can easily be disabled by setting `RATE_LIMIT=0/0` in `/etc/pihole/pihole-FTL.conf`. If I want, say, to set a rate limit of 1 query per hour, the option should look like `RATE_LIMIT=1/3600`.

https://docs.pi-hole.net/ftldns/configfile/#rate_limit

https://www.reddit.com/r/pihole/comments/osm2fn/psa_if_you_are_having_random_dns_resolution/