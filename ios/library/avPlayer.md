

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


