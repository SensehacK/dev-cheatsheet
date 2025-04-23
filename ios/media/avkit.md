# AVKit


Libraries involved
AVKit
AVFoundation
AVPlayer

## [Video Terminologies](video_terms.md)

## SwiftUI POC

SwiftUI + Video player to stream.
[hls-streaming-with-avkit-and-swiftui](https://www.createwithswift.com/hls-streaming-with-avkit-and-swiftui/)

## [DRM](DRM.md)

## [HLS](HLS.md)

## [AVPlayer](avPlayer.md)

## [AVAsset](avAsset.md)

## [avPlayerItem](avPlayerItem.md)

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

[apple dev | selecting_subtitles_and_alternative_audio_tracks](https://developer.apple.com/documentation/avfoundation/media_playback/selecting_subtitles_and_alternative_audio_tracks)

### Loading media data async

[apple dev | Loading media data asynchronously](https://developer.apple.com/documentation/avfoundation/media_assets/loading_media_data_asynchronously)


## Interview Questions

[InterviewPrep | AVPlayer](https://interviewprep.org/avplayer-interview-questions/)


## [Video Geeking](tools/apps#Geeking)

## Video Toolbox

[apple docs | video toolbox](https://developer.apple.com/documentation/videotoolbox)


## Reference

[Using AVFoundation to Play and Persist HTTP Live Streams](https://developer.apple.com/documentation/avfoundation/offline_playback_and_storage/using_avfoundation_to_play_and_persist_http_live_streams)

[Video article ios-fairplay-drm-integration](https://medium.com/@burak.oguz/ios-fairplay-drm-integration-with-different-use-cases-8aff3d4248dd)

[github project | drm-sample-player-ios](https://github.com/Axinom/drm-sample-player-ios)

[youtube | Video Kit UIKit delegate and public functions](https://www.youtube.com/watch?v=IVyy-VBU-Cc)
