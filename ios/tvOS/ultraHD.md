

## Playback



## Error


### 4K 1st Gen Apple TV Crash

guys I think so I figured out why - just why we have 4K playback issues with 1st gen apple 4K tv.  
A1842 - AppleTV6,2I went into some archives of apple newsroom and found this article where it clearly mentions that this newer gen [2nd apple tv 4K has A12 Bionic chip and it supports 4K HDR with High frame rate](https://www.apple.com/pt/newsroom/2021/04/apple-unveils-the-next-generation-of-apple-tv-4k/)So I opened up the `Olympics 4K` stream HLS file. Usually on traditional movies we have 23.7fps or 24fps. Only hobbit or handful of actual movies are shot at 60fps.  
But not being prevalent to Live TV | sports streaming culture in USA, I came to know that you guys have 60hz tv vs Europe having 50hz PAL vs NTSC or something (old stuff)  
& I predicted maybe `Olympics 4K` "Sports TV" content could be 60fps | hz as well. Voila! it was according to my novice understanding of HLS manifest formatting.

```ts
#EXT-X-STREAM-INF:BANDWIDTH=18104192,AUDIO="104192-mp4a.40.5",CLOSED-CAPTIONS="cc",FRAME-RATE=59.940,PROGRAM-ID=1,CODECS="hvc1.2.4.L153.90,mp4a.40.5",SUPPLEMENTAL-CODECS="dvh1.08.09/db1p",RESOLUTION=3840x2160,VIDEO-RANGE=PQ
OLYM4K_UD_02163/track-video-repid-trackId-101-tc-.m3u8
```


including the old HLS Olympics 4K stream for reference.So once in a blue moon - the error AVFoundation | AVKit gave us back is kinda true "false positive"  
It said incompatibleDisplay but it should have been `incompatibleSourceFrameRateFor4K`Tl;Dr: Apple 4KTV 1st gen old hardware 2017 - mo' bit rate | frames mo' heat ==> bad bad (CPU throttling)so apple never supported it and other 4K content usually is less than 30fps.  
Now I can enjoy my 4th of July ! @principal_engg @director2 



[Apple unveils the next generation of Apple TV 4K](https://www.apple.com/pt/newsroom/2021/04/apple-unveils-the-next-generation-of-apple-tv-4k/)

With A12 Bionic and the all-new Siri Remote, the best living room device gets even better. (37 kB)



P.S : sorry for late ping in the evening - just couldn't share this and close off. It all ties together why youtube was crashing on 4K videos. Because youtube videos have option for 4K at 30fps & 60fps. So my understanding is it was trying to play at higher frame rate + bitrate when network conditions are perfect -> but they had this error which was not handled by them just like PlayerPlatform had to do. Its just we were 2 - 3 years late because we never had this scenario as our content was never 4K @60fps.

References:

[apple newsroom 1st gen apple tv 4K](https://www.apple.com/newsroom/2017/09/apple-tv-4k-brings-home-the-magic-of-cinema-with-4k-and-hdr/)
no mention of high frame rate HDR or anything.

[apple HLS documentation supplemental codecs | Dolby Vision | HDR](https://developer.apple.com/documentation/http-live-streaming/hls-authoring-specification-for-apple-devices-appendixes#The-SUPPLEMENTAL-CODECS-attribute)
we were using `VIDEO-RANGE=PQ` which is `Dolby Vision`
```ts
CODECS="hvc1.2.4.L153.90,mp4a.40.5",
SUPPLEMENTAL-CODECS="dvh1.08.09/db1p",
RESOLUTION=3840x2160,
VIDEO-RANGE=PQ
```

[apple technical document for the device also mentions](https://support.apple.com/en-us/111929) so no HDR at 60fps support & we use Dolby Vision (HDR) protocol.
```markdown
### Video Formats

- H.264/HEVC SDR video up to 2160p, 60 fps, Main/Main 10 profile
    
- HEVC Dolby Vision (Profile 5)/HDR10 (Main 10 profile) up to 2160p
```