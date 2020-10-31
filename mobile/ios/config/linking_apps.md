# Linking Apps

## Deep link

Good tutorial on how to achieve this.

[Swift DC](https://www.swiftdevcenter.com/custom-url-scheme-deep-link-ios-13-and-later-swift-5/)

## Check App installation

With javascript we could redirect the navigation window object to a specific url of the app & if it doesn’t work we would just run the app store url of the app.

```javascript
setTimeout(function () { 
// Won't execute first due to timeout function
window.location = "https://itunes.apple.com/appdir"; }, 25);

window.location = "appname://";
```

[SO Link](https://stackoverflow.com/questions/13044805/how-to-check-if-an-app-is-installed-from-a-web-page-on-an-iphone?rq=1)

