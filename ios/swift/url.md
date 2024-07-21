# URL

## Intro

All things URL related in Swift.

## Syntax

```swift
guard let url = URL(string: playable.uri),
              (url.host != nil) else {
            throw CustomError(uri: playable.uri)
}
```

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

## URLQueryItem

```swift
let searchTerm = "obi wan kenobi"
let format = "wookiee"

var urlComponents = URLComponents()
urlComponents.scheme = "https"
urlComponents.host = "swapi.co"
urlComponents.path = "/api/people"
urlComponents.queryItems = [
   URLQueryItem(name: "search", value: searchTerm),
   URLQueryItem(name: "format", value: format)
]

print(urlComponents.url?.absoluteString) 
// https://swapi.co/api/people?search=obi%20wan%20kenobi&format=wookie
```

Reference code from this link
[building-safe-url-in-swift-using-urlcomponents-and-urlqueryitem](https://www.alfianlosari.com/posts/building-safe-url-in-swift-using-urlcomponents-and-urlqueryitem/)

[building-urls-with-urlqueryitem-in-swift](https://cocoacasts.com/building-urls-with-urlqueryitem-in-swift)

## URL Encoding

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
print(blogURL.absoluteString) 
// Prints: https://www.avanderlee.com/swift
```


ASCII to URL encoding
[eso org table](https://www.eso.org/~ndelmott/url_encode.html)


## File Path | FileManager API

Path of the file on system.

```swift
let url = URL(fileURLWithPath: path)
```

FileManager API

```swift
let folderURL = try FileManager.default.url(
            for: .documentDirectory,
            in: .userDomainMask,
            appropriateFor: nil,
            create: false
        )
```

[apple doc | File system programming guide](https://developer.apple.com/library/archive/documentation/FileManagement/Conceptual/FileSystemProgrammingGuide/AccessingFilesandDirectories/AccessingFilesandDirectories.html)

## Validation

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

[SO | how-to-check-validity-of-url-in-swift](https://stackoverflow.com/questions/28079123/how-to-check-validity-of-url-in-swift)

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

[SO | how-to-open-an-url-in-swift](https://stackoverflow.com/questions/39546856/how-to-open-an-url-in-swift)

[apple dev | url open](https://developer.apple.com/documentation/uikit/uiapplication/1648685-open)

## Caveats 

One of the Trakt TV Api I needed to use `addValue` instead of `setValue` Spent like 20 mins wondering why it is failing for me on VisionOS & Xcode 15 Beta 6.

Stack overflow and internet was not helpful stating to restart the simulator and Xcode beta issues of some kind.

```swift
var urlRequest = URLRequest(url: url)

urlRequest.setValue("Content-Type", forHTTPHeaderField: "application/json")

urlRequest.addValue("application/json", forHTTPHeaderField: "Content-Type")
```

Probably something related to adding it incrementally ? with `addValue` it works. Is it a Trakt TV API issue ? or maybe the async await API for URLSession.shared.data(urlRequest:) recommends this way of adding them content headers values to URLRequest.

## Download Task

```swift
let config = URLSessionConfiguration.background(withIdentifier: "com.example.DownloadTaskExample.background")

let session = URLSession(configuration: config, delegate: self, delegateQueue: OperationQueue())

let url = URL(string: "https://example.com/example.pdf")!
let task = session.downloadTask(with: url)
task.resume()
```

[Downloading files in background with URLSessionDownloadTask](https://www.ralfebert.com/ios-examples/networking/urlsession-background-downloads/)


## Diff between URI URN URL

> A URI can be further classified as a locator, a name, or both. The term "Uniform Resource Locator" (URL) refers to the subset of URIs that, in addition to identifying a resource, provide a means of locating the resource by describing its primary access mechanism (e.g., its network "location"). The term "Uniform Resource Name" (URN) has been used historically to refer to both URIs under the "urn" scheme [[RFC2141]](https://www.ietf.org/rfc/rfc2141.txt), which are required to remain globally unique and persistent even when the resource ceases to exist or becomes unavailable, and to any other URI with the properties of a name.

So all URLs are URIs, and all URNs are URIs - but URNs and URLs are different, so you can't say that all URIs are URLs.

[SO | reference ^](https://stackoverflow.com/a/176274/5177704)


## Reference

[A Comprehensive Guide to URLs in Swift and SwiftUI](https://matteomanferdini.com/swift-url-components/)

[apple dev | url components](https://developer.apple.com/documentation/foundation/urlcomponents)

[avanderlee | URL components](https://www.avanderlee.com/swift/url-components/)

[swift by sundell | Managing URLs and endpoints](https://www.swiftbysundell.com/clips/4/)

[swift by sundell | constructing-urls-in-swift](https://www.swiftbysundell.com/articles/constructing-urls-in-swift/)
