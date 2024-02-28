

## Placeholder color


iOS 15 & 16 above
```swift
TextField("", text: $viewModel.userName, prompt: Text("Phone, email or username").foregroundColor(.gray))
```
[SO | swiftui-how-to-change-the-placeholder-color-of-the-textfield](https://stackoverflow.com/questions/57688242/swiftui-how-to-change-the-placeholder-color-of-the-textfield)



## Alignment

```swift
VStack(alignment: .trailing) {
     Text("-\(value.author)")
}
.frame(maxWidth: .infinity, alignment: .trailing)
```

Giving full width of the device and then setting the alignment on VStack was the important in order to set the text inside to the right most / trailing location.

[SO | swiftui-text-alignment](https://stackoverflow.com/questions/56443535/swiftui-text-alignment)
