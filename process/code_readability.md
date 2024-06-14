
It is one of those things which goes hand in hand when compared to code perusing and peer reviewing PRs. It is important to understand the implication of having too much longer strings in a condition. Since not everyone has ultra wide screen monitors and even if for some reason we do. I like to setup mine with 3 Code windows in my IDE to quickly work through the code overall.


## Naming schemes

Naming appropriately with variables is important. Try to avoid appending the atype to the variable since the IDE can always show quick help or infer those types automatically with its tooltip option + click.

> Less is more.


## Two many characters on same line

Also when you refactor this in a function.  
Make sure all your conditional checks are on a separate lines.  
It's easier for reader to quickly check all the conditions.

Old code 

```swift
if let manifestUrl = asset?.manifestUrl, let comLocationPostalCode = asset?.comLocationPostalCodeString, let comDeviceType = asset?.comDeviceTypeString  {
    asset?.manifestUrl = "\(manifestUrl)sz=\(comLocationPostalCode)&sz=\(comDeviceType)"
}
```

New code
```swift
if let manifestUrl = asset?.manifestUrl,
   let comLocationPostalCode = asset?.comLocationPostalCodeString, 
   let comDeviceType = asset?.comDeviceTypeString  {
     asset?.manifestUrl = "\(manifestUrl)sz=\(comLocationPostalCode)&sz=\(comDeviceType)"
}
```

### Another example of Ultra wide *code*

```swift
NotificationCenter.default.post(name:NSNotification.Name(rawValue: CustomName), object: player, userInfo: [CustomName_SIGNAL_ID:"x",CustomName_STREAM_ID:"1"])
```

```swift
NotificationCenter
.default
.post(name: NSNotification.Name(rawValue: CustomName), 
	  object: player,
	  userInfo:[
	  CustomName_SIGNAL_ID:"x",
	  CustomName_STREAM_ID:"1"
	  ]
)
```

more readable rather than one liner and I do have ultra wide monitor but I split my code editors in x3 format so this makes it easier to read and review while on mobile, iPad, or portrait screens like a browser tabs 2/3 of space.

### Reactive Paradigm Flow

Stylistic nitpick: 
Could break the part after `?.` output .... on respective lines for easier code reading.
Its harder to keep up with more than 2 access like `= , . , { , :`  on a single line.

```swift
lifeCycleCancellable = eventOrchestrator?.output.errorEvent.sink(receiveValue: { [weak self] in
	self?.eventOrchestrator?.input.handleError.send(($0, false))
        })
```

```swift
lifeCycleCancellable = eventOrchestrator?
	.output
	.errorEvent
	.sink { [weak self] in
		self?.eventOrchestrator?
			.input
			.handleError
			.send(($0, false))
    }
```
## Parameters naming

Code snippet in review
```swift
static func customPlayer(with asset: Asset, authAPI: customAuth) throws -> PlayerConstruction {|
	return try PlayerDirector.construct(with: asset, drmAuthorizer: customAuth) 
}
```

Stylistic comment

I usually don't like to change params being passed around too much. 
Since we now have `authAPI`, `drmAuthorizer` If you want it named `drmAuthorizer` internally maybe having similar external param could help and internally reference same. 


Since while reading from `.construct()` it just gets more hazy with 3 diff names -> of course `customAuth` param value might always change depending on the managed solution construction but we can always control the `params` internal / external.


### Bloated Initializer with Long Array or list

Question: 
> But wouldn't adding a comment also suffice unless we are using this allowList elsewhere?

Old code
```swift
init() { 
	self.bus.add(observer: self, for: [.adQProgress,
            .assetSourceChanged,
            .adEvent,
            .bufferingStarted,
            .bufferingCompleted,
            .esp,
            .error,
            .fragmentWarning,
            .seekStarted,
            .seekCompleted,
    ])
}
```
New code
```swift
init() { 
	let allowedEventTypes: [CustomBusEventType] = [
            .adQProgress,
            .assetSourceChanged,
            .adEvent,
            .bufferingStarted,
            .bufferingCompleted,
            .esp,
            .error,
            .fragmentWarning,
            .seekStarted,
            .seekCompleted,
        ]
    self.bus.add(observer: self, for: allowedEventTypes)	 
}
```

My reasoning: 


Rather than adding comments every time, sometimes having a variable succinct enough to make the code readable in the `init` makes it easier for the code breakage and structurally having a mind map of what is going on.  
In this case you can go either way but since the init had a long list of array having it as a variable makes it more easier for future `git diffs` or `adding more things to the array` or `being independent from an overloaded` init()` while reading it.