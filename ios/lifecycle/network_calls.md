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




## [URL](url.md)

## Reference 

[swift by Sundell | Generic network APIs](https://www.swiftbysundell.com/articles/creating-generic-networking-apis-in-swift/)

