

## Issues

### Certificate OVPN

Last time I had similar issue with VPN Unlimited changing something with 
[VPN Unlimited changed their CA](https://github.com/haugene/vpn-configs-contrib/issues/261)

Until this gets fixed on the repo (all .ovpn files must be updated), you can temporarily create your own updated .ovpn file and use custom provider in the configuration as explained in
What I did on my setup is this workaround :

1. Copy the currently used .ovpn file from this repo and replaced `<ca> <cert> and <key>` inside using the values from a freshly generated .ovpn file from vpnunlimited web account manager.
2. Put this file in a folder on your host machine that will be mounted in your container to `/etc/openvpn/custom` as stated in the documentation.
3. Change docker env var `OPENVPN_PROVIDER` to `custom`

### 2025 OVPN

```log
2025-03-03 22:04:00 SIGTERM[soft,tls-error] received, process exiting
Modification: Change tls-crypt keyfile path
Modification: Set output verbosity to 3
Modification: Remap SIGUSR1 signal to SIGTERM, avoid OpenVPN restart loop
Modification: Updating status for config failure detection
Setting OpenVPN credentials...
adding route to local network 10.0.0.0/24 via 172.18.0.1 dev eth0
2025-03-03 21:54:44 DEPRECATED OPTION: --cipher set to 'AES-256-CBC' but missing in --data-ciphers (AES-256-GCM:AES-128-GCM). Future OpenVPN version will ignore --cipher for cipher negotiations. Add 'AES-256-CBC' to --data-ciphers or change --cipher 'AES-256-CBC' to --data-ciphers-fallback 'AES-256-CBC' to silence this warning.
2025-03-03 21:54:44 OpenVPN 2.5.9 arm-unknown-linux-gnueabihf [SSL (OpenSSL)] [LZO] [LZ4] [EPOLL] [PKCS11] [MH/PKTINFO] [AEAD] built on Sep 29 2023
2025-03-03 21:54:44 library versions: OpenSSL 3.0.2 15 Mar 2022, LZO 2.10
2025-03-03 21:54:44 NOTE: the current --script-security setting may allow this configuration to call user-defined scripts
2025-03-03 21:54:44 TCP/UDP: Preserving recently used remote address: [AF_INET]195.154.199.175:1194
2025-03-03 21:54:44 Socket Buffers: R=[212992->212992] S=[212992->212992]
2025-03-03 21:54:44 UDP link local: (not bound)
2025-03-03 21:54:44 UDP link remote: [AF_INET]195.154.199.175:1194
2025-03-03 21:54:44 TLS: Initial packet from [AF_INET]195.154.199.175:1194, sid=f3d26b82 438e4fae
2025-03-03 21:54:45 VERIFY ERROR: depth=1, error=self-signed certificate in certificate chain: C=US, ST=NY, L=New York, O=Simplex Solutions Inc., OU=Vpn Unlimited, CN=server.vpnunlimitedapp.com, name=server.vpnunlimitedapp.com, emailAddress=support@simplexsolutionsinc.com, serial=12327878784855983598
2025-03-03 21:54:45 OpenSSL: error:0A000086:SSL routines::certificate verify failed
2025-03-03 21:54:45 TLS_ERROR: BIO read tls_read_plaintext error
2025-03-03 21:54:45 TLS Error: TLS object -> incoming plaintext read error
2025-03-03 21:54:45 TLS Error: TLS handshake failed
2025-03-03 21:54:45 SIGTERM[soft,tls-error] received, process exiting
```

[docker-transmission-openvpn | issuecomment-2688580491](https://github.com/haugene/docker-transmission-openvpn/issues/2923#issuecomment-2688580491)

[docker-transmission-openvpn | Issue 2923](https://github.com/haugene/docker-transmission-openvpn/issues/2923)

[Error due to port updated on SSL](https://github.com/qdm12/gluetun/commit/0b078e5f5eb275d514ba8069e40958bc8c56d7a4)

Also updated new `.opvn` config file 

[Single VPN Custom locator](https://haugene.github.io/docker-transmission-openvpn/supported-providers/#using_a_local_single_ovpn_file_from_a_provider) 

Had to use [linux user_root](os/linux/user_root) Root file manager to edit these config files.
Using GUI not command line approach
Created a new directory named `mar_2025` and in that copied the `.opvn` file named `mar_2025` 

```docker
## New Custom config
- OPENVPN_PROVIDER=custom
- OPENVPN_CONFIG=mar_2025
volumes:
	- /etc/openvpn/mar_2025:/etc/openvpn/custom/
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

- [LunaSea](https://www.lunasea.app/)
- nzb360

## Mind Map

[open_vpn](open_vpn.md)

[portainer](portainer.md)