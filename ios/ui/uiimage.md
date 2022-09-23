UIImage


## Setup

Assigning the image data value to a specific image outlet object.
> self.UIImage_name.image = UIImage(data: data)


## Download Image

Make an extension for downloading images using URL or string and updating the main UIImage object or outlet with the image data object.
```swift
extension UIImageView {
    func downloaded(from url: URL, contentMode mode: UIView.ContentMode = .scaleAspectFit) {
        contentMode = mode
        
        // Creating URL Request
        var request = URLRequest(url: url)
        request.httpMethod = "GET"
        
        // Setting API Key
        request.setValue(Constants.apiKey.rawValue, forHTTPHeaderField: Constants.apiHeader.rawValue)
        
        URLSession.shared.dataTask(with: request) { (data, response, error) in
            guard
                let httpURLResponse = response as? HTTPURLResponse, httpURLResponse.statusCode == 200,
                let mimeType = response?.mimeType, mimeType.hasPrefix("image"),
                let data = data, error == nil,
                let image = UIImage(data: data)
                else {
                print("Error retrieving data")
                return }
            DispatchQueue.main.async() { [weak self] in
                self?.image = image
            }
        }.resume()
    }
    func downloaded(from link: String, contentMode mode: UIView.ContentMode = .scaleAspectFit) {
        guard let url = URL(string: link) else { return }
        downloaded(from: url, contentMode: mode)
    }
}
```

[SO](https://stackoverflow.com/questions/24231680/loading-downloading-image-from-url-on-swift)
[](https://cocoacasts.com/fm-3-download-an-image-from-a-url-in-swift)

## Programmatic UI Image


[article](https://www.appsdeveloperblog.com/create-uiimage-and-uiimageview-programmatically/)
[SO](https://stackoverflow.com/questions/26569371/how-do-you-create-a-uiimage-view-programmatically-swift)
[](http://webindream.com/how-to-add-uiimageview-programmatically-in-swift/)