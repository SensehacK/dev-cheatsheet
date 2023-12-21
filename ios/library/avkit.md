# AVKit


Libraries involved
AVKit
AVFoundation
AVPlayer


## SwiftUI POC

SwiftUI + Video player to stream.
[hls-streaming-with-avkit-and-swiftui](https://www.createwithswift.com/hls-streaming-with-avkit-and-swiftui/)

## [DRM](DRM.md)

## [HLS](HLS.md)

## [AVPlayer](avPlayer.md)


## AVPlayerItem

## Guides

### Video thumbnail

This below snippet code should be able to extract the thumbnail image from the given video source. We can also create random time value to generate different thumbnails but we have ensure that the video is at least 13 secs long in this code snippet. You can safe guard yourself with a range of video duration and generate random thumbnail out of it. 

```swift
let asset = AVAsset(url: url)
let avAssetImageGen = AVAssetImageGenerator(asset: asset)
avAssetImageGen.appliesPreferredTrackTransform = true

let thumbnailSnapTime = CMTimeMake(value: 13, timescale: 1)
do { 
   let thumbCGImage = try avAssetImageGen
   .copyCGImage(at: thumbanailSnaptime, actualTime: nil)
   let thumbImage = UIImage(cgImage: thumbCGImage)
} catch {
	print(error)
}
```


### Multiple Tracks 

https://developer.apple.com/documentation/avfoundation/media_playback/selecting_subtitles_and_alternative_audio_tracks

## Quirks

[impossible-to-stop-avplayer](https://stackoverflow.com/questions/32993896/impossible-to-stop-avplayer?noredirect=1&lq=1)


### Blank Video but audio audible

iOS 16.4 simulator bug for `HLS` streams. Confirmed on Apple developer website. Spent around 20 mins debugging what is wrong with my code overall.

[My own project POC](https://github.com/SensehacK/swift/tree/master/swiftUI/VideoContent)


## Interview Questions

[InterviewPrep | AVPlayer](https://interviewprep.org/avplayer-interview-questions/)


## Video Geeking

Codec - HEVC x265 - fav
Dolby Vision vs HDR10
4:4:4 DCI - Color accuracy
HLS - components sending data, easily quality switchable, streams m3u8 format
DASH MPD
HDMI 2.0 vs 2.1 
40Gbps vs 48Gbps
4K @120hz or 8K @60Hz
Apple Macbook pro 2023 M2Pro | Max finally has HDMI 2.1
Fav TV tech - LG OLEDs C3, G3 - 
Fav Video reviewer - [HDTVTest](https://www.youtube.com/@hdtvtest)
Fav games technical analysis - Digital Foundry
Rting website for nitty gritty comparison of Video tech.
[video tools - apps](apps.md#Video%20Tools)



## Reference

[Awesome Video Github repo](https://github.com/krzemienski/awesome-video/)

[Using AVFoundation to Play and Persist HTTP Live Streams](https://developer.apple.com/documentation/avfoundation/offline_playback_and_storage/using_avfoundation_to_play_and_persist_http_live_streams)

[Video article ios-fairplay-drm-integration](https://medium.com/@burak.oguz/ios-fairplay-drm-integration-with-different-use-cases-8aff3d4248dd)

[github project | drm-sample-player-ios](https://github.com/Axinom/drm-sample-player-ios)

[youtube | Video Kit UIKit delegate and public functions](https://www.youtube.com/watch?v=IVyy-VBU-Cc)


