## Normal Alert
```swift
struct ContentView: View {
    @State private var showingAlert = false

    var body: some View {
        Button("Show Alert") {
            showingAlert = true
        }
        .alert("Important message", isPresented: $showingAlert) {
            Button("OK", role: .cancel) { }
        }
    }
}
```


https://www.hackingwithswift.com/quick-start/swiftui/how-to-show-an-alert


## Destructive Alert

```swift
Button("Show Alert with Destruction") {
		destructiveAlert = true
	}
	.alert("Title", isPresented: $destructiveAlert, actions: {
		Button("Delete", role: .destructive, action: {
			print("Do something destructive")
		})
	}, message: {
		Text("Alert with Destructive option")
	})
```


https://sarunw.com/posts/how-to-present-alert-in-swiftui-ios15/