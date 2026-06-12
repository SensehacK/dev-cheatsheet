
## Exploit Patch Launcher Manager


- Download & install [Launcher Manager](https://xdaforums.com/attachments/lm_1-1-1-apk.6275902/) app (v1.1.1).  
    **Downloader code:** 2370884
- Through ADB run the following command to give it the required permissions:  
    `pm grant com.wolf.tn android.permission.WRITE_SECURE_SETTINGS`

```sh
pm grant com.wolf.tn android.permission.WRITE_SECURE_SETTINGS
```

[Source XDA Forum Tools](https://xdaforums.com/t/system-user-fireos7-os8-all-fire-cubes-sticks-televisions-tablets.4759215/)



**Manual Instructions through ADB**  

1. Enable ADB debugging in FireOS  
    FireOS Settings > My Fire TV > Developer options > ADB debugging > on  
      
    **NOTE:** If Developer options isn't showing, open About, select Fire TV [Cube/Stick] and tap select 7x to unhide developer menu.


## Reset blacklist apps


```sh
settings delete global hidden_api_blacklist_exemptions
```


## Disable OTA firmware
  
**Disable OTA firmware updates [FIRE TV]**  

```sh
pm disable com.amazon.device.software.ota
pm clear com.amazon.device.software.ota
pm disable com.amazon.device.software.ota.override
pm disable-user com.amazon.sneakpeek
pm disable com.amazon.client.metrics
sync
```

NOTE: verify com.amazon.device.software.ota is still disabled after rebooting. List all disabled apps:

`pm list package -d`


## Set a custom launcher 

[FIRE TV]

```sh
pm disable com.amazon.firehomestarter
pm disable com.amazon.tv.launcher
```


Press Home button on remote, select your installed custom launcher from the popup at the buttom of the screen.  
  
**NOTE:** You will no longer be able to access FireOS settings after disabling Amazon Launcher