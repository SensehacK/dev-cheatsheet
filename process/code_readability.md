
It is one of those things which goes hand in hand when compared to code perusing and peer reviewing PRs. It is important to understand the implication of having too much longer strings in a condition. Since not everyone has ultra wide screen monitors and even if for some reason we do. I like to setup mine with 3 Code windows in my IDE to quickly work through the code overall.


## Naming schemes

Naming appropriately with variables is important. Try to avoid appending the type to the variable since the IDE can always show quick help or infer those types automatically with its tooltip option + click.

Less is more.


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