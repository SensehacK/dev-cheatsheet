# DRM

## Lot of different options

- WideVine
- Axinom DRM
- [Apple's FairPlay HLS](https://en.wikipedia.org/wiki/FairPlay)
- https://developer.apple.com/streaming/fps/
- [BrightCove SDK](https://sdks.support.brightcove.com/getting-started/native-video-playback.html)

## [Apple Fairplay](fairplay.md)

## Errors

## HDCP 

HDCP is a form of DRM that's baked into the HDMI standard. If you're watching media that uses it on a device that isn't compliant, you'll get a black screen. I have a splitter that I use to strip it myself because I have have one of those cheap Chinese projectors, and my cable box refuses to work with it otherwise.
[Source of this comment ^](https://www.reddit.com/r/Piracy/comments/d0v8cd/comment/ezgaroq/?utm_source=share&utm_medium=web2x&context=3)

## [Video Tools](tools/apps.md#Video%20Tools)

## Anti DRM

[scene ripping process context amazon / netflix](https://torrentfreak.com/the-scene-pirates-ripping-content-from-amazon-netflix-190707/)


### DRM Stripping

[how-to-strip-drm-from-wtv](https://www.avsforum.com/threads/how-to-strip-drm-from-wtv.1514421/)

[ripping-streaming-video](https://forum.redfox.bz/threads/ripping-streaming-video.72106/)

## Tagging

[forensic-watermarking](https://help.moxion.io/article/121-forensic-watermarking)

## Headers

### PSSH

[Protection System Specific Header](https://docs.axinom.com/services/drm/technical-articles/pssh/) 


## License

We can have one license requests for different tracks.
eg. 1 audio
1 video
1 subtitle? (idk didnt confirm)


So it will make the necessary network request to the MDS server which will give us the appropriate license -> result for decrypting or SPC keys to plug into the Fairplay SDK.
[fairplay](fairplay.md)


Sometimes we can multiple DRM tiers in the same asset, 
eg. Video
360p - 560p DRM tier 1
720p - 1080p DRM tier 2
1440p - 2160p DRM tier 3

due to various licensing, or server / business logic / compute available. 

In this scenario, you might see AVKit or Apple [abr](abr.md), at first start with `lowest` or `default` quality tier and then approach to ramp up / down the bitrates / resolution given the network conditions suffice the playback for seamless UX with no extra buffering, thermal state, networking range, battery etc., IDK what inputs are put in this mix and AVKit is a blackbox for us, so won't be able to comment on its internal logic on how it decides to switch up / down with the streaming.

So after it has pre buffered enough 5 - 10 secs and has enough network to support higher tiers, it can make subsequent `license` requests for getting the DRM key -> MDS flow.

[Fairplay Flow](fairplay.md#Flow)

## References

[How DRM works video](https://www.youtube.com/watch?v=mn2POYEiJVE)

[avplayer-swiftui-player-controls](https://chris-mash.medium.com/avplayer-swiftui-part-2-player-controls-c28b721e7e27)

[playing-video-avplayer-swiftui](https://benoitpasquier.com/playing-video-avplayer-swiftui/)


