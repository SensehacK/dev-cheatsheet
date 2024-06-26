# DRM

## Lot of different options

- WideVine
- Axinom DRM
- [Apple's FairPlay HLS](https://en.wikipedia.org/wiki/FairPlay)
- https://developer.apple.com/streaming/fps/
- [BrightCove SDK](https://sdks.support.brightcove.com/getting-started/native-video-playback.html)

## Apple Fairplay

DRM is pretty poorly documented, at least Apple's Fairplay solution.
[this article is somewhat helpful](https://ottverse.com/apple-fairplay-streaming-drm-how-does-it-work/)

[Playing Encrypted HLS content on iOS using swift](https://assist-software.net/snippets/how-play-encrypted-http-live-streams-offline-avfoundation-ios-using-swift-4)

## Errors

### FairPlay Streaming is not supported on simulators

You need to disable fairplay streaming on simulators to run it appropriately.

```sh
*** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '*** -[AVContentKeySession initWithKeySystem:storageDirectoryAtURL:legacyWebKitCompatibilityMode:] FairPlay Streaming is not supported on simulators'
```


## HDCP 

HDCP is a form of DRM that's baked into the HDMI standard. If you're watching media that uses it on a device that isn't compliant, you'll get a black screen. I have a splitter that I use to strip it myself because I have have one of those cheap Chinese projectors, and my cable box refuses to work with it otherwise.
[Source of this comment ^](https://www.reddit.com/r/Piracy/comments/d0v8cd/comment/ezgaroq/?utm_source=share&utm_medium=web2x&context=3)

## [Video Tools](apps.md#Video%20Tools)

## Anti DRM

[scene ripping process context amazon / netflix](https://torrentfreak.com/the-scene-pirates-ripping-content-from-amazon-netflix-190707/)

[Reddit | Piracy wiki](https://www.reddit.com/r/piracy/wiki/faq/)

### DRM Stripping

[how-to-strip-drm-from-wtv](https://www.avsforum.com/threads/how-to-strip-drm-from-wtv.1514421/)

[ripping-streaming-video](https://forum.redfox.bz/threads/ripping-streaming-video.72106/)

## Tagging

[forensic-watermarking](https://help.moxion.io/article/121-forensic-watermarking)

## References

[How DRM works video](https://www.youtube.com/watch?v=mn2POYEiJVE)

[avplayer-swiftui-player-controls](https://chris-mash.medium.com/avplayer-swiftui-part-2-player-controls-c28b721e7e27)

[playing-video-avplayer-swiftui](https://benoitpasquier.com/playing-video-avplayer-swiftui/)

[Apple DRM how does it work](https://ottverse.com/apple-fairplay-streaming-drm-how-does-it-work/)

[Wiki | FairPlay](https://en.wikipedia.org/wiki/FairPlay)
