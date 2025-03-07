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



## Optimization


You can call `AVPlayer.play()` even when there is no AVPlayerItem in the player yet. Player records intention and when you attach playerItem, you save few milliseconds because player doesn't need to generate static image.


## Sound

A playback category should not obey the mute switch

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
	try? AVAudioSession.sharedInstance()
	.setCategory(AVAudioSession.Category.playback)
	try? AVAudioSession.sharedInstance()
	.setActive(true)
}
```

[SO | Make sound in vibrate DND mode](https://stackoverflow.com/questions/40089891/avplayer-does-not-sound-if-disabled-audio-vibration-on?noredirect=1&lq=1)

In case you end up here, because this solution won't work on iPad, but only on iPhone: I just had that issue when setting the `AVAudioSession` category before presenting a `AVPlayerViewController`. If I set the category in the completion block of the `presentViewController` call (and before actually calling `play()`) it works fine on both device families.




## AVPlayerLayer

3 Steps
- Wrap it in `UIViewRepresentable` to have compatibility from UIKit to SwiftUI.
- Make subclass of `UIView` with private instance of `AVPlayerLayer()` 
- Show it in `some View` struct swiftUI - call it from step 1 view created.

[SO | avplayer in vstack swiftUI](https://stackoverflow.com/questions/56822943/how-to-show-my-avplayer-in-a-vstack-with-swiftui)


## PiP

Picture in Picture support

I don't think AVPlayer needed to do anything for PiP, too. There is audio focus handling but that's separate.
As long as appropriate flags are being set, we can utilize this native functionality provided by apple iOS / iPadOS.

## Reference


[Apple Old | AVFoundation Programming Guide](https://developer.apple.com/library/archive/documentation/AudioVideo/Conceptual/AVFoundationPG/Articles/02_Playback.html)

[playing-video-avplayer-swiftui](https://benoitpasquier.com/playing-video-avplayer-swiftui/)

[AVPlayer SwiftUI | Github](https://github.com/ChrisMash/AVPlayer-SwiftUI?tab=readme-ov-file)
