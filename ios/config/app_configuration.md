# App Configuration


## Intro

Configuring your app with important data when the app is launched is one of the crucial steps of App Launch lifecycle

```swift
struct AppConfig {
	let bundleId: String
	let environment: String
	let policy: String
	let support: String
	let copyright: String
	let website: String
}
```

## Init

Having two initializers for invoking the app config is also nicer to have so that you don't add too much fluff on App initialization

```swift
init(
	bundleId: String = "",
	company: String = "",
	environment: String = "",
	privacyPolicy: String = "",
	support: String = "") {
		self.company = company
}

init(bundle: Bundle = Bundle.main) { 
	guard let plist = bundle.infoDictionary,
    let company = plist[Keys.AppName.companyName] as? String else {
	    return makeHardCodedAppConfig()
    }
	self.company = company
}
```