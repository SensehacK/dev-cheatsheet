
## Troubleshooting

Use a network sniffer / firewall - man in the middle attack which snoops all your network requests.
I recommend [these apps](tools/apps#Debugging). 

[debug hls streams](https://www.fastpix.io/blog/how-to-troubleshoot-hls-live-stream-in-ios)

# AV Media | Foundation | Player Errors

## AVKit

### Impossible to stop AVPlayer

[impossible-to-stop-avplayer](https://stackoverflow.com/questions/32993896/impossible-to-stop-avplayer?noredirect=1&lq=1)

### Blank Video but audio audible

iOS 16.4 simulator bug for `HLS` streams. Confirmed on Apple developer website. Spent around 20 mins debugging what is wrong with my code overall.

[My own project POC](https://github.com/SensehacK/swift/tree/master/swiftUI/VideoContent)


## AVPlayer

### Core Media 12746

This error happened to me on Macbook Pro 16, macOS Sequioa, Xcode 16.2.0 beta 6, iOS 18.2 simulator. Playing a apple's test HLS AV asset Advance web stream.

```error
CoreMediaErrorDomain Code=-12746
Printing description of playerError:
▿ UnknownPlayerError
  - errorId : "UnknownPlayerError"
  - description : "AVPlayer Item Status Changed"
  - component : "com.nitro.core"
  ▿ context : 2 elements
    ▿ 0 : 2 elements
      - key : "NSLocalizedDescription"
      - value : "AVPlayer Item Status Changed"
    ▿ 1 : 2 elements
      - key : "NSUnderlyingError"
      - value : Error Domain=CoreMediaErrorDomain Code=-12746 "(null)"
  ▿ cause : Optional<Error>
```


Solution
- Kill `coreAudio` service or task running in background, Activity monitor.
- Kill simulator
- run the project again.

[SO | avPlayer-failure-hls](https://stackoverflow.com/questions/62362804/avplayer-failure-with-hls-live-stream-url-on-tvos-13-4-works-on-tvos-13-3)


### CoreMediaErrorDomain error -16845 

```error
- HTTP 429: (unhandled)), Error Status Code: -16845

```

This occurred due to [HTTP 429](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status/429)

```
https://cdn.bitmovin.com/content/assets/sintel/hls/playlist.m3u8
Traffic rate limit of fair-use exceeded.
```


## Reference

[good AVKit errors gist](https://gist.github.com/Ali72/cbde769d4bbf55390c8dcfb97a81f6f4)

