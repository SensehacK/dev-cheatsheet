



## Fixed Frame

Always wrap your `AsyncImage` block of code into a Stack and give it a fixed frame so that it can automatically expand when making network requests for getting images.
```swift
VStack {
	AsyncImage(url: meal.image) { image in
		image
			.resizable()
			.aspectRatio(contentMode: .fit)
			.cornerRadius(Constants.cornerRadius)
	} placeholder: {
		ProgressView()
	}
}
.frame(width: 100, height: 100)
```

This below code will sometimes not have images initialized or downloaded. So they will be truncated and no image or placeholder would be shown. We don't want that to be the case. So having a fixed frame to the cell images is prefered with the above snippet of code does. TIL.
```swift
AsyncImage(url: meal.image) { image in
	image
		.resizable()
		.frame(width: 100, height: 100)
		.aspectRatio(contentMode: .fit)
		.cornerRadius(Constants.cornerRadius)
} placeholder: {
	ProgressView()
}
```


## AsyncImagePhase

Image caching in memory is one of those nicer things to have. I recently implemented similar approach of NSCache with dictionary based caching.
[cache](ios/lifecycle/cache.md)