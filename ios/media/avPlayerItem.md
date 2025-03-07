# AVPlayerItem




## Resolution


If you want to have a specific bitrate to be targeted by the AVFoundation library.

Apple has a property `.preferredpeakbitrate` which you can use to guide the system to try its best to achieve that.

[apple - docs | AVPlayerItem](https://developer.apple.com/documentation/avfoundation/avplayeritem/1388541-preferredpeakbitrate)


## Monitor playback


[media playback](https://developer.apple.com/documentation/avfoundation/media_playback/monitoring_playback_progress_in_your_app)

Get current Asset duration and playhead position or time in seek position

```swift
if let currentItem = player.currentItem {
    let duration = CMTimeGetSeconds(currentItem.duration)
    let currentTime = CMTimeGetSeconds(currentItem.currentTime())

    print("Duration: \(duration) s")
    print("Current time: \(currentTime) s")
}
```

## Seek

HLS Event Style playlist with live and VOD content.
Seeking at initial start point - [github thread](https://github.com/video-dev/hls.js/issues/284)

`EXT-X-START:TIME-OFFSET=x`


[apple docs old | Event Style Playlist](https://developer.apple.com/library/archive/technotes/tn2288/_index.html#//apple_ref/doc/uid/DTS40012238-CH1-EVENT_PLAYLIST)