


## Windows 

You can have a flat 2D window display like an ipad app as well as insert volumetric 3D assets to show AR or 3D objects in AR/VR environment.

[apple dev | windows#visionOS](https://developer.apple.com/design/human-interface-guidelines/windows#visionOS)

## Immersive View

[Vision OS iPad Mode](https://forums.developer.apple.com/forums/thread/736592)


## Images 

Image Views on VisionOS needs to provide appropriate information to display image assets.
[apple dev | image-views#visionOS](https://developer.apple.com/design/human-interface-guidelines/image-views#visionOS)


## swift UI 

[swift with majid | swiftUI vision OS](https://swiftwithmajid.com/2024/01/23/introducing-swiftui-on-visionOS/)



## Ornaments

These look cool and you can have multiple ornaments for an app outside or attached to your app window boundary.
Game changer for sure adds more depth and gives more option to the developer or end user to add more space to the content being showed and can excuse the attached toolbars.
[apple dev | ornaments](https://developer.apple.com/design/human-interface-guidelines/ornaments)


[swift with majid | ornaments](https://swiftwithmajid.com/2024/01/30/visionos-ornaments-in-swiftui/)



## Errors

### Previews Compilation error

```log
Ambiguous use of 'init'
```

I solved it using 
```swift
#if os(visionOS)
#Preview(windowStyle: .automatic) {

}
#endif
```