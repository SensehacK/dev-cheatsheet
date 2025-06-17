

## Intro

Great tool for 21st century with proper macos UI mechanisms.
This works 100% of the time for getting my iOS or networking debugging things work for me.


## Official documentation

[docs.proxyman.io](https://docs.proxyman.io/)



SSL proxying

[docs | ssl-proxying](https://docs.proxyman.io/basic-features/ssl-proxying)


Breakpoints support
[docs | breakpoint-for-ios](https://docs.proxyman.io/proxyman-ios/breakpoint-for-ios)



## Open source CLI tool

[mitmproxy](https://mitmproxy.org/) 

```sh
brew install mitmproxy
```

## tvOS

If you want to configure for a physical tvOS apple tv 4K, you need few things to set it up.

- [Apple Configurator | app store](https://apps.apple.com/us/app/apple-configurator/id1037126344)
- Proxyman
- Apple TV 4K
- Same Wifi network with manual DHCP address reservation
- [node package manager](../tools/terminal/node#Node%20Version%20Manager)

### Steps

- download proxyman `downloadedProfile.pem` from “[http://proxy.man/ssl](http://proxy.man/ssl)” & rename it to `downloadedProfile.cer`
- Apple configurator -> File -> New Profile -> Name the profile "customTVOS_proxy" -> Select "Wifi", click "Configure"
- Fill your usual Wifi SSID (name: WifiName) & make sure `Proxy Setup` is selected to manual with provided `ProxyMan` Server and Port address eg. `10.0.0.22:9090`
- select “Certificates” → Click “Configure” → upload the `downloadedProfile.cer` file that you previously downloaded & renamed.
- save the profile `tvOSProxyProfile.mobileconfig` at accessible location & open a terminal at that `$pwd`
- Run a temporary [http server](../tools/server/http-server#Node) using node
- Make sure appleTV is on the same Wifi network 2.4 or 5Ghz and open Settings -> General -> Privacy & Security -> Share Apple TV Analytics. Press apple tv remote physical button `Play/Pause` new window will appear.
- Select `Add Profile`, add the mac http server ip address with port and local file complete path. eg: `http://10.0.0.22:8033/tvOSProxyProfile.mobileconfig` (easier to copy paste from mac shared clipboard to iPhone + tv remote Input prompt)
- Select "Install", few times and then we need to trust the certificate by heading over to Settings -> General ->   About ->   Certificate Trust Settings ->   Click on Proxy Profile ->   “Continue”.
- You may need to reenter your WiFi credentials again since for me it got disconnected once with tvOS 17.0 - apple TV 4K 2023.

Now you can see the logs of Apple tv 4K on Proxy man. I believe similar steps could be performed for [Charles proxy](network/charles_proxy.md)



## Versions

Free version is sufficient overall


I might consider upgrading to `Premium` version just to support them.

