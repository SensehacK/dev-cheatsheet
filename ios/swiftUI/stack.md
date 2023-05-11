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

## Examples

Line Wrapping stacks

https://swiftui.diegolavalle.com/posts/linewrapping-stacks/


Lazy Stacks

https://www.appcoda.com/swiftui-lazyvgrid-lazyhgrid/

## Error



```swift
Couldn't add LazyVStack { 
	HStack { } // Errors out
}
```
It always needed VStack only 