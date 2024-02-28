
Structs are Views in Swift UI. So they need to be initialize and can't be mutated. In order to mutate them in the SwiftUI app lifecycle you need to mark it as `@State`


## Errors

###  Cannot assign to property: 'self' is immutable

So swiftUI view definition is internally a struct. So by default it is immutable.

So we need to use a special property wrapper called `@State` in order to make the compiler / run time executioner know about the exception for this.

```swift
struct TracksView: View {
	private var runCount = 0
	// vs
	@State private var runCount = 0

	var body: some View { }
}
```

[HWS | explanation](https://www.hackingwithswift.com/quick-start/swiftui/how-to-fix-cannot-assign-to-property-self-is-immutable)



### convert value type expected binding type

[HWS | how-to-fix-cannot-convert-value-of-type-string-to-expected-argument-type-binding-string](https://www.hackingwithswift.com/quick-start/swiftui/how-to-fix-cannot-convert-value-of-type-string-to-expected-argument-type-binding-string)


