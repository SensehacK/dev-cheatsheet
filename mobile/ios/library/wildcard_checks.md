# Wildcard checks


## Check OS version

```swift

guard #available(iOS 14, *) else {
    print("Returning if iOS 13 or lower")
    return
}

print("This code only runs on iOS 14 and up")

```

[@available / #available](https://www.avanderlee.com/swift/available-deprecated-renamed/)