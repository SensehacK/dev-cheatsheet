# Cocoapods syntax





## removing cocoapods generated pods and cache


[Source](https://stackoverflow.com/questions/45306087/cocoapods-is-installing-old-pod-version)
You could try the following:
Clearing CocoaPods' cache:

    rm -rf "${HOME}/Library/Caches/CocoaPods"
    rm -rf "`pwd`/Pods/" (while in your project's dir)
    Finally pod update

If you are using 0.38.0.beta1, you can just use pod cache clean
Regenerate everything:

    rm -rf ~/Library/Caches/CocoaPods
    rm -rf Pods; rm -rf ~/Library/Developer/Xcode/DerivedData/*
    pod deintegrate; pod setup; pod install
