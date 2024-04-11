



Using Reality Kit to make 2D - 3D experiences with video assets to play videos without extra control to the user.
[apple dev | RealityKit](https://developer.apple.com/documentation/RealityKit)

https://developer.apple.com/documentation/realitykit/videoplayercomponent



## HID 

Vision OS recommendation for playing video in the UI xrOS.
[apple dev |  playing-video#visionOS](https://developer.apple.com/design/human-interface-guidelines/playing-video#visionOS)



## 3D Playback

By utilizing a utility tool by Michael Swanson

[Spatial video tool blog by Michael Swanson](https://blog.mikeswanson.com/post/744337392062873601/spatial-video)

```sh
spatial make -i test_sbs_1080p.mp4 -f ou -o new_spatial.mov --cdist 19.24 \
--hfov 63.4 --hadjust 0.02 --primary right --projection rect
```

[Documentation for CLI spatial tool](https://blog.mikeswanson.com/spatial)

Had issues playing 3D video on simulator


```log
App VideoPlayer+Component Caption: onComponentDidUpdate Media Type is invalid

PVC/0-0 Received playback error: [Error Domain=AVFoundationErrorDomain Code=-11833 "Cannot Decode" UserInfo={NSUnderlyingError=0x600000d25560 {Error Domain=CoreMediaErrorDomain Code=-12906 "(null)"}, NSLocalizedFailureReason=The decoder required for this media cannot be found., AVErrorMediaTypeKey=vide, NSLocalizedDescription=Cannot Decode}]

PVC/0-0 <ObjectIdentifier(0x00000001079267c0)>Enter-Fullscreen error handler: CancellationError()

PVC/0-0 transition 'enterFullscreen' failed with [CancellationError()] (LinearMediaKit/FullscreenPresenter.swift:1236)
```

I believe it worked fine on actual vision Pro device.

### Apple docs

Apple documentation around conversion of 3D SBS movies
[Converting side-by-side 3D video to multiview HEVC](https://developer.apple.com/documentation/avfoundation/media_reading_and_writing/converting_side-by-side_3d_video_to_multiview_hevc#4334336)


## References

[apple dev | adopting_the_system_player_interface_in_visionos](https://developer.apple.com/documentation/avkit/adopting_the_system_player_interface_in_visionos)
