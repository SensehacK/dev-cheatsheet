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

[HWS | how-to-show-an-alert](https://www.hackingwithswift.com/quick-start/swiftui/how-to-show-an-alert)



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


[sarunw | how-to-present-alert-in-swiftui-ios15](https://sarunw.com/posts/how-to-present-alert-in-swiftui-ios15/)


## Nuances

iPad (reg width screen class) confirmation dialog needs to be anchored to the view providing interaction.

```swift
// Old 
List {
	CatalogItemView(item: item) {
		selectedCatalogItem = item
		isConfirmingDownload = true
	}
}
.confirmationDialog { } // UI dialogue
.navigationTitle("Items")

// New
CatalogItemView(item: item) {
	selectedCatalogItem = item
	isConfirmingDownload = true
}
.confirmationDialog { }
```