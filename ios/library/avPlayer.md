# AVPlayer

## Listeners

Observer to see when the video playback **started**

```swift
player = AVPlayer(url: URL(fileURLWithPath: path))
player.addObserver(self, forKeyPath: "rate", options: NSKeyValueObservingOptions.new, context: nil)

override func observeValue(forKeyPath keyPath: String?, of object: Any?, change: [NSKeyValueChangeKey : Any]?, context: UnsafeMutableRawPointer?) {
    if keyPath == "rate" {
        if player.rate > 0 {
            print("video started")
        }
    }
}
```

[Knowing when AVPlayer object is ready to play](https://stackoverflow.com/questions/5401437/knowing-when-avplayer-object-is-ready-to-play)

[How to detect AVPlayer actually started to play in swift](https://stackoverflow.com/questions/40781738/how-to-detect-avplayer-actually-started-to-play-in-swift)

### [How to detect user selection of subtitles when using AVPlayerViewController](https://stackoverflow.com/questions/49412371/how-to-detect-user-selection-of-subtitles-when-using-avplayerviewcontroller)


## Selecting Tracks AV Media Playback

[Selecting Subtitles and Alternative Audio Tracks](https://developer.apple.com/documentation/avfoundation/media_playback/selecting_subtitles_and_alternative_audio_tracks)

[AVAsset](https://developer.apple.com/documentation/avfoundation/avasset)

[Media playback](https://developer.apple.com/documentation/avfoundation/media_playback)


## Muting Audio


```
```

```swift
if IsMuted == false {
      IsMuted = true
      musicPlayer.volume = 0
    } else {
      IsMuted = false
      musicPlayer.volume = 1
    }
}
```