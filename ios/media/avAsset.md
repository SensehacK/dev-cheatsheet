# AVAsset | AVAssetTrack

## Intro


## Syntax

## Retrieve Media Metadata

[Retrieving media metadata](https://developer.apple.com/documentation/avfoundation/media_assets/retrieving_media_metadata)


## Extract Media Codec information

[apple dev | formatDescriptions](https://developer.apple.com/documentation/avfoundation/avpartialasyncproperty/3816116-formatdescriptions)

[SO | retrieving codec iOS](https://stackoverflow.com/a/36655446/5177704)
[Another SO](https://stackoverflow.com/questions/62218974/is-there-any-way-to-determine-what-codec-avplayer-is-using)


## video size

[SO | ios video size](https://stackoverflow.com/questions/37943008/how-to-get-video-size-for-hls-stream-inside-avplayer)

```swift
import AVKit
import Foundation

extension AVAsset {
    func videoSize() async throws -> CGSize? {
        guard let track = try await loadTracks(withMediaType: .video).first else { return nil }
        let size = try await track.load(.naturalSize)
        return size
    }
}
```