

## Issues

Last time I had similar issue with VPN Unlimited changing something with 
[VPN Unlimited changed their CA](https://github.com/haugene/vpn-configs-contrib/issues/261)

Until this gets fixed on the repo (all .ovpn files must be updated), you can temporarily create your own updated .ovpn file and use custom provider in the configuration as explained in
What I did on my setup is this workaround :

1. Copy the currently used .ovpn file from this repo and replaced `<ca> <cert> and <key>` inside using the values from a freshly generated .ovpn file from vpnunlimited web account manager.
2. Put this file in a folder on your host machine that will be mounted in your container to `/etc/openvpn/custom` as stated in the documentation.
3. Change docker env var `OPENVPN_PROVIDER` to `custom`

docker container error for [docker tranmission open vpn](https://github.com/haugene/docker-transmission-openvpn?tab=readme-ov-file) repo
```error
2025-04-02 00:59:47 VERIFY ERROR: depth=2, error=self-signed certificate in certificate chain: C=US, ST=NY, L=New York, O=KeepSolid Inc., OU=KeepSolid VPN Root CA, CN=KeepSolid VPN Root CA, emailAddress=admins@keepsolid.com, serial=590830292952905902500539248317331898854520058318
2025-04-02 00:59:47 OpenSSL: error:0A000086:SSL routines::certificate verify failed
2025-04-02 00:59:47 TLS_ERROR: BIO read tls_read_plaintext error
2025-04-02 00:59:47 TLS Error: TLS object -> incoming plaintext read error
2025-04-02 00:59:47 TLS Error: TLS handshake failed
2025-04-02 00:59:47 SIGTERM[soft,tls-error] received, process exiting
```


### File copy issues

Either do `sudo pacman` or use ssh file copy 

```sh
sudo scp local_filePath.ovpn /etc/openvpn
```

## Custom Config

[Using a local single .ovpn file from a provider](https://haugene.github.io/docker-transmission-openvpn/supported-providers/#external_providers)

[Configs](https://github.com/haugene/vpn-configs-contrib/tree/main/openvpn)

[Official Configs from Transmission](https://github.com/transmission/transmission/blob/main/docs/Editing-Configuration-Files.md#options)


```sh
## Transmission Config
- TRANSMISSION_WEB_UI=transmission-web-control
- TRANSMISSION_DOWNLOAD_DIR=/downloading
- TRANSMISSION_INCOMPLETE_DIR=/incomplete
- TRANSMISSION_WATCH_DIR=/downloads_watch
- TRANSMISSION_SPEED_LIMIT_UP=100
- TRANSMISSION_SPEED_LIMIT_UP_ENABLED=true
- TRANSMISSION_RATIO_LIMIT=0.2
- TRANSMISSION_RATIO_LIMIT_ENABLED=true
```

## Apps

- LunaSea
- nzb360


## Mind Map

[open_vpn](open_vpn.md)

[portainer](portainer.md)