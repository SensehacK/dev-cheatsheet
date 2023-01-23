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

## Concurrent Image Load

Copied from the solution: 
```text

1.  This code isn't thread safe, because you have race condition on `numImagesLoaded`. This could, theoretically, result in `continueLoad` to be called more than once. You can achieve thread safety by synchronizing `numImagesLoaded` by dispatching updates to this (and other model objects) back to the main queue.
    
2.  Like DashAndRest said, you have to dispatch the UI update to the main queue, as well.
    
3.  When you made this asynchronous, you introduced a network timeout risk when you initiate a lot of requests. You can solve this by refactoring the code to use operation queues instead of dispatch queues and specify `maxConcurrentOperationCount`.
    
4.  The images are being added to an array:
    
    -   Because these tasks run asynchronously, they're not guaranteed to complete in any particular order, and thus the array won't be in order. You should save the images in a dictionary, in which case the order no longer matters.
        
    -   Just like `numImagesLoaded`, the `pieceImages` isn't thread safe.
        
5.  You are using a lot of forced unwrapping, so if any requests failed, this would crash.
But to address this, we have to step back and look at the routine calling this method. Let's imagine that you have something like:
```

```swift
var pieceImages = [UIImage()]

func loadAllImages() {
    for imageUrl in imageURLs {
        imageLocXML(imageUrl)
    }
}

func imageLocXML(il:String) {
    dispatch_async(dispatch_get_global_queue(QOS_CLASS_USER_INITIATED, 0)) {
        let url:NSURL? = NSURL(string: il)
        let data:NSData? = NSData(contentsOfURL: url!)
        let image = UIImage(data: data!)
        self.pieceImages.append(image!)
        self.numImagesLoaded += 1
        self.updateProgressBar()
        if self.numImagesLoaded == self.numImagesToLoad {
            self.continueLoad()
        }
    }
}
```

I'm suggesting that you replace that with something like:

```swift
var pieceImages = [String: UIImage]()

func loadAllImages() {
    let queue = NSOperationQueue()
    queue.maxConcurrentOperationCount = 4

    let completionOperation = NSBlockOperation {
        self.continueLoad()
    }

    for imageURL in imageURLs {
        let operation = NSBlockOperation() {
            if let url = NSURL(string: imageURL), let data = NSData(contentsOfURL: url), let image = UIImage(data: data) {
                NSOperationQueue.mainQueue().addOperationWithBlock {
                    self.numImagesLoaded += 1
                    self.pieceImages[imageURL] = image
                    self.updateProgressBar()
                }
            }
        }

        queue.addOperation(operation)
        completionOperation.addDependency(operation)
    }

    NSOperationQueue.mainQueue().addOperation(completionOperation)
}
```
https://stackoverflow.com/questions/37885623/using-dispatch-async-to-load-images-in-background

## Programmatic UI Image


[article](https://www.appsdeveloperblog.com/create-uiimage-and-uiimageview-programmatically/)
[SO](https://stackoverflow.com/questions/26569371/how-do-you-create-a-uiimage-view-programmatically-swift)
[](http://webindream.com/how-to-add-uiimageview-programmatically-in-swift/)


## Vector Image

Supporting vector - scalable image asset in iOS

Using `Preserve Vector Data` property in Assets option in the inspector tab.
Good article about its usage.
https://useyourloaf.com/blog/xcode-9-vector-images/