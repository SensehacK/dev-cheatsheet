
# HLS

## Intro

Every HLS file has these properties

```ts
#EXTM3U
#EXT-X-VERSION:4
```

## [HLS Playlist Types](HLS_types.md)

## De-Muxed | Muxing

## Test Streams

[developer.apple.com/streaming/examples/](https://developer.apple.com/streaming/examples/)

```js
dash: 'https://cdn.bitmovin.com/content/assets/sintel/sintel.mpd'
hls:'https://cdn.bitmovin.com/content/assets/sintel/hls/playlist.m3u'
```

[Apple HLS examples - bib bop advance HEVC](https://devstreaming-cdn.apple.com/videos/streaming/examples/bipbop_adv_example_hevc/master.m3u8)

[Apple HLS examples - Multiple audio and subtitles](https://devstreaming-cdn.apple.com/videos/streaming/examples/adv_dv_atmos/main.m3u8)

[Apple HLS examples - bib bop normal](https://devstreaming-cdn.apple.com/videos/streaming/examples/img_bipbop_adv_example_fmp4/master.m3u8)

HLS stream having :  
. 6 video qualities for Adaptive Bitrate  
. 2 alternate audio tracks (English and French)  
. 3 alternate subtitle tracks (English, English with audio description and French)
[Link](https://sample.vodobox.com/planete_interdite/planete_interdite_alternate.m3u8)



## HLS Keys

### TARGET DURATION

This sets the playlist or the video processor that all the components `.mp4` or `.ts` or segments of audio/video/text are of specific secs. In this example the target segments are of `10 secs` each.

```ts
#EXT-X-TARGETDURATION:10

#EXTINF:10.0,
fileSequenceA.ts
#EXTINF:10.0,
fileSequenceB.ts
```

So if the targetDuration is higher then the avPlayer library would take some time to buffer first 2 - 3 fragments and then resume. 
So `10 secs * 2` so 20 secs of content. This is what I assume I understand from my conversation about this.


### CONTENT METADATA


Protocol `HLSTagDescriptor` and `HLSTagValueIdentifier`

`HLSTagDescriptor` = EXT-X-XCAL-CONTENTMETADATA  |  the tag name
`HLSValueIdentifier` = KEYID | DRMAGNOSTIC | the attribute names in the tag

```ts
#EXT-X-XCAL-CONTENTMETADATA:KEYID="bd8e7d69-saw4-6a00-1eb9-637364ad6a4c",DRMAGNOSTIC="ZXlKNE5YUWpVekksa3r3XXzNFTnZrSFE="
```

## Techniques

### Switch Live to Event Record

When I think of an EVENT style playlist in streaming world, I think of DVR | Video Recordings. If a user is scrolling the Live Grid in video stream app and they want to record an episode, that playlist will go from `LIVE` -> `EVENT`. Best way to see this is to select a live program, hit Record, wait until the UI says the recording is set. Next, hit Watch and you'll see the `Live` HLS manifest file  program is now `Event`

## Thumbnails

```ts
#EXT-NOM-I-FRAME-DISTANCE
```

## Advertising

```ts
#EXT-X-ADVERTISING:SYSCODE=231532523532377442
```

## DRM

```ts
#EXT-X-XCAL-CONTENTMETADATA:
KEYID="017ee539-UUID-string",
DRMAGNOSTIC="some_base_64_key_value"
```

## Apple Interstitials

[Getting Started With HLS Interstitials - apple developer](https://developer.apple.com/streaming/GettingStartedWithHLSInterstitials.pdf)

Other


## Low Latency

[apple | ll-hls](https://developer.apple.com/documentation/http-live-streaming/enabling-low-latency-http-live-streaming-hls)


## References

[apple docs | HLS](https://developer.apple.com/documentation/http-live-streaming)

[what-is-hls-video-streaming-and-how-does-it-work](https://api.video/blog/video-trends/what-is-hls-video-streaming-and-how-does-it-work/)

[hls-http-live-streaming-how-does-it-work](https://ottverse.com/hls-http-live-streaming-how-does-it-work/)

[what-is-hls-streaming-and-how-do-you-deploy-it](https://www.cardinalpeak.com/blog/what-is-hls-streaming-and-how-do-you-deploy-it)

[http-live-streaming](https://www.dacast.com/blog/http-live-streaming/)

[hls-streaming-protocol](https://www.dacast.com/blog/hls-streaming-protocol/)

[apple developer | doc archive | HLS Overview](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/StreamingMediaGuide/UsingHTTPLiveStreaming/UsingHTTPLiveStreaming.html)

[github  public test videos HLS](https://gist.github.com/jsturgis/3b19447b304616f18657)


## Specifications

[HLS content steering | apple specs](https://developer.apple.com/streaming/HLSContentSteeringSpecification.pdf)




## Highest quality

video - 0 = is the highest quality in the HLS format.


## Playback

[Improving playback on HLS](https://www.brightcove.com/de/resources/blog/improving-hls-playback/)


[hls - optimize performance](https://www.theoplayer.com/blog/optimizing-ll-hls-4-key-factors-affecting-its-performance)


## Tools 


[N_m3u8DL-CLI github](https://github.com/nilaoda/N_m3u8DL-CLI)

[Stream detector](https://github.com/54ac/stream-detector)

[hls downloader](https://github.com/puemos/hls-downloader)

[stream recorder download](https://chromewebstore.google.com/detail/stream-recorder-download/iogidnfllpdhagebkblkgbfijkbkjdmm?pli=1)

[hls analyzer | cloud](http://hlsanalyzer.com)

[apple HLS validator](https://developer.apple.com/documentation/http-live-streaming/using-apple-s-http-live-streaming-hls-tools)

This gives us a debug analysis of the stream in question to validate whether its a stream issue or our player code issue.

```sh
mediastreamvalidator https://314.linear-ag-xcr/v1/frag/bmff/enc/wea/t/OsaK_UD_T_7381_0_7683.m3u8
```

After that it will create a json file which we can ingest into the hlsreport tool.

```sh
hlsreport validation_data_4K_superbowl.json
```

[wwdc | hls tools](https://developer.apple.com/videos/play/wwdc2016/510/?time=543)

## streams

Test streams provided for HLS testing or playback.
### Apple

[hls examples](https://developer.apple.com/streaming/examples/)

### Third Party 

[github | hls-test-streams](https://github.com/bengarney/list-of-streams?tab=readme-ov-file)

### Spatial 3D HLS

[historic_planet_content 3D video](https://devstreaming-cdn.apple.com/videos/streaming/examples/historic_planet_content_2023-10-26-3d-video/DoVi_P20_34000_t2160p/prog_index.m3u8)

## Troubleshooting

Use a network sniffer / firewall - man in the middle attack which snoops all your network requests.
I recommend [these apps](tools/apps#Debugging). 



[debug hls streams](https://www.fastpix.io/blog/how-to-troubleshoot-hls-live-stream-in-ios)