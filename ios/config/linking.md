# Linking

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



## Universal Links


Supporting Universal links on iOS requires you to have access to Apple developer account, website domain, subdomain, write file access to public folder, SSL certificate for website to host over `https`. 

It is a time consuming process but when configured properly it is seamless to work with. Since you won't have to worry about checking if the app is installed on the user device. Apple takes care of those underlying logic. With Deep linking apple first opens the URI callback on default web browser - Safari and then makes the call to open the app if installed. This requires very less effort.
But with Universal links apple is able to directly open the link on the app if supported.


[Setting up Universal links](https://www.branch.io/resources/blog/how-to-setup-universal-links-to-deep-link-on-apple-ios/) Source: Branch-IO

Apple documentation

- [Allowing apps and websites to link to your content](https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content?language=objc)
- [Supporting universal links in your app](https://developer.apple.com/documentation/xcode/supporting-universal-links-in-your-app?language=objc)


- [Supporting associated domains](https://developer.apple.com/documentation/xcode/supporting-associated-domains?language=objc)
Note
If your site uses multiple subdomains (such as `example.com`, `www.example.com`, and `support.example.com`), each requires its own entry in the [`Associated Domains Entitlement`](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_associated-domains), and each must serve its own `apple-app-site-association` file.

Subdomain help
https://asbelita.medium.com/manage-universal-links-with-multiple-associated-domains-in-ios-97bda851b654

## Testing


Opening links without typing it in simulator for testing can be easily achieved using Xcode CLI.


Use this command to launch website or URL on simulator

```bash
xcrun simctl openurl booted "https://reddit.com/"

xcrun simctl openurl booted "com.trackvia://"
```


https://isapozhnik.com/articles/6-ways-of-launching-deeplinks-on-ios-simulator/