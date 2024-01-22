

## Debugging

Enable SSL proxying for specific URLs or wildcards if needed.


## Process

Charles generates a `.pem` file - Privacy Enhanced Mail (PEM)
How `.pem` file differs from regular old OpenSSL key file - good thread to read [here](https://serverfault.com/questions/9708/what-is-a-pem-file-and-how-does-it-differ-from-other-openssl-generated-key-file)

```pem
-----BEGIN CERTIFICATE-----
MIIFVjCCBD6gAwIBAgIGAYlG5S1aMA0GCSqGSIb3DQEBCwUAMIGvMUAwPgYDVQQDDDdDaGFybGVz+VY=
-----END CERTIFICATE-----
```



Generating one is easy while using fastlane tool on macOS
https://docs.fastlane.tools/actions/pem/


##  Troubleshooting

### My internet connection doesn't work

Probably your Charles proxy server is being deallocated from the memory by OS schedulers. Check `Task Manager | Activity Monitor` just to see if the app is still consuming and listening for network events properly.

### Charles Profile doesn't download certificate `.pem` file

For me reinstalling the app and restarting the iPhone usually helps.
But to be extra cautious, check whether you have added `0.0.0.0/0` to the 
`Proxy > Access Control Settings` to give access to all the devices trying to route their proxy network traffic and give all iPv4 range table access to be allowed by default. It makes you avoid that pesky `Allow | Deny` confirmation dialogue box for the `Access Control Settings`
Also double check `Allow List` in Tools Menu is being enabled, disable that option if you don't want a whitelisted option for specific domains.


### Charles Profile doesn't show up on iOS Settings App
It is likely that your default browser is not `Safari` Apple kinda makes it PITA to always use their proprietary browser in order to do configuration profiles or certificates installs. I was using Firefox on iOS (Internal engine is still safari WebView WebKit Engine) with default browser selected as well since `Deeplinks` usually don't work on non default browser sometimes. But opening it on Safari with website `http://chls.pro/ssl` worked for me this time.


### Network requests shows `unknown` data

You need to go to Settings -> General -> About -> Certificate Trust Settings and toggle `Enable Full Trust for Root Certificates`

### Can no longer browse Internet without Charles

[charles proxy FAQ steps](https://www.charlesproxy.com/documentation/faqs/can-no-longer-browse-without-charles-running/)

### video playback buffering

```sh
DelioPlayer Media Failed. Description:1012.10 (Fairplay DRM):`The DRM delegate failed to acquire a license. (Delio)` Context: `(DelioPlayer) DRM Error` Delio Error Info 9004: `DelioError code:couldNotAcquireLicense.(9004)
assetURL:[http://ccr.linear-tve-ashburn-](http://ccr.linear-tve-sa-vss.top.sa.net/v1/frag/bmff/enc/cbcs/t/.m3u8?sz=urn:scte:224:audience:Zip:21412)


errorDescription" : "1001.2 (General Errors):`An unspecified network error occurred.` Context: `(DelioPlayer) Delio Error` Delio Error Info 4003: `DelioError code:playlistDeliveryUnableToDeliverPlaylist.
```

Turns out de-provisioning the security DRM client on the physical device solved this issue. Logging out and back works.

## Resources

[Kodeco | charles-proxy-tutorial-for-ios](https://www.kodeco.com/21931256-charles-proxy-tutorial-for-ios)


[Charles Proxy blocking SSL traffic on Android](https://stackoverflow.com/questions/53197681/charles-proxy-blocking-ssl-traffic-on-android)

