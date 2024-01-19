
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

### TARGETDURATION

This sets the playlist or the video processor that all the components `.mp4` or `.ts` or segments of audio/video/text are of specific secs. In this example the target segments are of `10 secs` each.

```ts
#EXT-X-TARGETDURATION:10

#EXTINF:10.0,
fileSequenceA.ts
#EXTINF:10.0,
fileSequenceB.ts
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

## References

[what-is-hls-video-streaming-and-how-does-it-work](https://api.video/blog/video-trends/what-is-hls-video-streaming-and-how-does-it-work/)

[hls-http-live-streaming-how-does-it-work](https://ottverse.com/hls-http-live-streaming-how-does-it-work/)

[what-is-hls-streaming-and-how-do-you-deploy-it](https://www.cardinalpeak.com/blog/what-is-hls-streaming-and-how-do-you-deploy-it)

[http-live-streaming](https://www.dacast.com/blog/http-live-streaming/)

[hls-streaming-protocol](https://www.dacast.com/blog/hls-streaming-protocol/)

[apple developer | doc archive | HLS Overview](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/StreamingMediaGuide/UsingHTTPLiveStreaming/UsingHTTPLiveStreaming.html)