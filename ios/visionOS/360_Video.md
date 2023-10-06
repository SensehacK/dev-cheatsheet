

## Code Snippet 

https://developer.apple.com/forums/thread/734081

Hello, It is very easy to represent a 360° Video in the Vision Pro environment.

1. You have to create videoPlayer
2. create a very big sphere I recommend a sphere with the size 1E3 (1* 10^3)
3. assign a VideoMaterial to this entity
4. adjust the properties of the entity for your needs and add some videoPlayer controls to your video if it is you want.

Here is a simple approach and a little code snippet:

```swift
//Create Entity for the video
let videoEntity = Entity()

//Search for video in paths
guard let url = Bundle.main.url(forResource: "example", withExtension: "mp4") else {fatalError("Video was not found!")}

//create a simple AVPlayer
let asset = AVURLAsset(url: url)
let playerItem = AVPlayerItem(asset: asset)
let player = AVPlayer()

//create a videoMaterial
let material = VideoMaterial(avPlayer: player)

//Made a Sphere with the videoEntity and asign the videoMaterial to it
videoEntity.components.set(ModelComponent(mesh: .generateSphere(radius: 1E3), materials: [material]))

//adjust the properties of the videoEntity(Sphere) if needed
videoEntity.scale = .init(x: 1, y: 1, z: -1)
videoEntity.transform.translation += SIMD3<Float>(0.0, 10.0, 0.0)

let angle = Angle.degrees(90)
let rotation = simd_quatf(angle: Float(angle.radians), axis: .init(x: 0, y: 0, z: 0))

videoEntity.transform.rotation = rotation

//add VideoEntity to realityView
content.add(videoEntity)

//start the VideoPlayer
player.replaceCurrentItem(with: playerItem)
player.play()
}
```

I would recommend actually to use a video which was actually designed for 360° view :) I hope I could help you :)



## 360 Photography

https://www.dpreview.com/articles/0778031862/apple-vision-pro-what-it-means-for-content-and-photography



## Libraries

For 360 images

https://github.com/Ssimboss/Image360

https://github.com/robbykraft/Panorama