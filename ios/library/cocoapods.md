# Cocoapods

Cocoapods is a library package manager for swift, way before Swift package manager was a thing. Many swift libraries were available using cocoapods “pod file”.

## Errors

### Removing cocoapods generated pods and cache

[Source](https://stackoverflow.com/questions/45306087/cocoapods-is-installing-old-pod-version)

You could try the following: Clearing CocoaPods' cache:

```text
> rm -rf "${HOME}/Library/Caches/CocoaPods"
> rm -rf "`pwd`/Pods/" (while in your project's dir)
> pod update
```

If you are using 0.38.0.beta1, you can just use pod cache clean

Regenerate everything:

```text
> rm -rf ~/Library/Caches/CocoaPods
> rm -rf Pods
> rm -rf ~/Library/Developer/Xcode/DerivedData/*
> pod deintegrate
> pod setup
> pod install
```

### CDN sources issue

While running ```pod install`` you may encounter some cocoa pods dependency errors and I would document a few of those.

Error

> Couldn’t find compatible version

```text
[!] CocoaPods could not find compatible versions for pod "Mapbox-iOS-SDK":
  In Podfile:
    Mapbox-iOS-SDK (~> 5.9)
```

You could just run the command which is been suggested by Cocoapods CLI itself

`pod install --repo-update`

I had to change the CDN source due to the issue of Cocoapods dirty tree history [Link](https://blog.cocoapods.org/CocoaPods-1.7.2/) Stack Overflow discussion [here](https://stackoverflow.com/a/58577253)

