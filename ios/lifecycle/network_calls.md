# Network


## API Calls

### Step 1

Make structure to conform with codable data type

### Step 2

Make asynchronous network calls with specific URL

### Step 3

Add header files and authorization to the network request being created and sent over from apple default URLSession


```swift
guard let url = URL(string: Constants.baseURL.rawValue + Constants.image.rawValue + value) else { return  }
        
	// ImageResponse(name: "Billy", url: "https://i.redd.it/vxyig96zgfh61.png", type: "png", width: 400, height: 400)
	// Creating URL Request
	var request = URLRequest(url: url)
	request.httpMethod = "GET"
	
	// Setting API Key
	request.setValue(Constants.apiKey.rawValue, forHTTPHeaderField: Constants.apiHeader.rawValue)
	
	let task = URLSession.shared.dataTask(with: request) { (data, response, error) in
		guard error == nil else { return }
		
		guard let httpResponse = (response as? HTTPURLResponse)?.statusCode, httpResponse == HTTPStatusCode.statusSuccess.rawValue else {
			let httpCode = (response as? HTTPURLResponse )?.statusCode
			print("Error in retrieving data from API", +httpCode!)
			if httpCode == HTTPStatusCode.statusUnauthorized.rawValue {
				print(Connection.statusUnauthorized.rawValue)
			}
			DispatchQueue.main.async {
				// TODO: Create a small popup alert stating error in retrieving data so the user is informed with the process.
			}
			return
		}

		guard let data = data else { return }
		do {
			imgResponse = try JSONDecoder().decode(ImageResponse.self, from: data)
			guard let imgResponse = imgResponse else {
				return
			}
			print(imgResponse.name)
			print(imgResponse.url)
//                return imgResponse
			DispatchQueue.main.async {
				completionHandler(imgResponse)
//                    return imgResponse
			}
		} catch let error {
			print("Error in retrieving data" + error.localizedDescription)
		}
		
		
	}

	// Resume Asynchronous network call
	task.resume()
```


Or you could just directly use `URL`

```swift
let task = URLSession.shared.dataTask(with: URL) { (data, response, error) in 
		  
}
```

dataTaskWithURL vs downloadTaskWithURL
First one downloads in memory / RAM and the other one downloads the file and stores it on local storage - of the device.
## URL Components

Constructing URLs using URL Components is much nicer and lets us have `preconditionFailure` in guard statements.

```swift
public func createSignUpURL(matching clientID: String = "clientID") -> URL {
	var components = URLComponents()
	components.scheme = "https"
	components.host = "qa1.qa.drive.com"
	components.path = "/#/sync"
	components.queryItems = [
	URLQueryItem(name: "client_id", value: clientID)
	]
	let finalURL = components.string?.removingPercentEncoding ?? "https://qa1.qa.drive.com/#/sync?client_id=clientID"
	
	return URL(string: finalURL)!
}
```

Source swift by sundell
```swift
var url: URL {
	var components = URLComponents()
	components.scheme = "https"
	components.host = "api.myapp.com"
	components.path = "/" + path
	components.queryItems = queryItems

	guard let url = components.url else {
		preconditionFailure(
			"Invalid URL components: \(components)"
		)
	}

	return url
}
```

## Checks

Checking if URL is valid form

```swift
// Swift 5
func verifyUrl (urlString: String?) -> Bool {
    if let urlString = urlString {
        if let url = NSURL(string: urlString) {
            return UIApplication.shared.canOpenURL(url as URL)
        }
    }
    return false
}
```

https://stackoverflow.com/questions/28079123/how-to-check-validity-of-url-in-swift

```swift
guard let url = URL(string: "http://www.google.com") else {
  return //be safe
}

if #available(iOS 10.0, *) {
    UIApplication.shared.open(url, options: [:], completionHandler: nil)
} else {
    UIApplication.shared.openURL(url)
}
```

https://stackoverflow.com/questions/39546856/how-to-open-an-url-in-swift
https://developer.apple.com/documentation/uikit/uiapplication/1648685-open


## URL encoding

Spaces -> percent encoding ` ` -> `%20`
```swift
let urlEncoded = value.addingPercentEncoding(withAllowedCharacters: .alphanumerics)
let url = "http://www.example.com/?name=\(urlEncoded!)"
```

Adding base path 

```swift
let category = "swift"
let baseURL = URL(string: "https://www.avanderlee.com")!
let blogURL = URL(string: category, relativeTo: baseURL)!
print(blogURL) // Prints: swift -- https://www.avanderlee.com
print(blogURL.absoluteString) // Prints: https://www.avanderlee.com/swift
```



## Reference 

https://developer.apple.com/documentation/foundation/urlcomponents

https://www.swiftbysundell.com/articles/constructing-urls-in-swift/

Managing URLs and endpoints
https://www.swiftbysundell.com/clips/4/

URL components base path
https://www.avanderlee.com/swift/url-components/

Generic network APIs
https://www.swiftbysundell.com/articles/creating-generic-networking-apis-in-swift/
