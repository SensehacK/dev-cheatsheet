# Stack

## Info

Three types of stacks - ZStack, VStack and HStack
## Code

Wrap any kind of view in stack content view.

```swift
VStack {
	Text(UIConstants.shanksText)
	
	Link(destination: URL(string: "https://onepiece.fandom.com/wiki/Shanks")!) {
		Label("Read More", systemImage: "flag.fill")
			.bold()
			.font(.title)
			.frame(width: 350, height: 50)
			.background(.red)
			.foregroundColor(.white)
			.cornerRadius(8)
	
	}	
}
.padding(20)
```

## ZStack

Z - axis of the swiftUI application. Typically used for displaying something over on background view of the application. 3D view. `Z.-1, Z.0, Z.+1`

Loading indicator could be on `+1`
UIButton could be on `0`
VStack or UITableView or UIBackground could be on `-1`


```swift
ZStack { 
	VStack { }
}
```

## Examples

Line Wrapping stacks

[linewrapping-stacks](https://swiftui.diegolavalle.com/posts/linewrapping-stacks/)


Lazy Stacks

[appcoda | swiftui-lazyvgrid-lazyhgrid](https://www.appcoda.com/swiftui-lazyvgrid-lazyhgrid/)


## Error



```swift
Couldn't add LazyVStack { 
	HStack { } // Errors out
}
```
It always needed VStack only 