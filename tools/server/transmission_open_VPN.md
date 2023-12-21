

## Issues

Last time I had similar issue with VPN Unlimited changing something with 
[VPN Unlimited changed their CA](https://github.com/haugene/vpn-configs-contrib/issues/261)

Until this gets fixed on the repo (all .ovpn files must be updated), you can temporarily create your own updated .ovpn file and use custom provider in the configuration as explained in
What I did on my setup is this workaround :

1. Copy the currently used .ovpn file from this repo and replaced `<ca> <cert> and <key>` inside using the values from a freshly generated .ovpn file from vpnunlimited web account manager.
2. Put this file in a folder on your host machine that will be mounted in your container to `/etc/openvpn/custom` as stated in the documentation.
3. Change docker env var `OPENVPN_PROVIDER` to `custom`

## Custom Config

[Using a local single .ovpn file from a provider](https://haugene.github.io/docker-transmission-openvpn/supported-providers/#external_providers)

[Configs](https://github.com/haugene/vpn-configs-contrib/tree/main/openvpn)

## Mind Map

[open_vpn](open_vpn.md)

[portainer](portainer.md)