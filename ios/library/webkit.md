## Webview

WKWebKit, UIWebKit
WebView


## References

https://www.appypie.com/wkwebview-how-to#Responding


https://www.hackingwithswift.com/example-code/wkwebview/how-to-control-the-sites-a-wkwebview-can-visit-using-wknavigationdelegate

https://www.hackingwithswift.com/articles/112/the-ultimate-guide-to-wkwebview

https://stackoverflow.com/questions/48689702/intercept-link-clicks-in-wkwebview

https://diamantidis.github.io/2020/02/02/two-way-communication-between-ios-wkwebview-and-web-page

https://nemecek.be/blog/1/how-to-open-target_blank-links-in-wkwebview-in-ios

https://designcode.io/swiftui-advanced-handbook-wkwebview


https://stackoverflow.com/questions/46254037/wkwebview-on-link-click-listener

https://medium.com/john-lewis-software-engineering/ios-wkwebview-communication-using-javascript-and-swift-ee077e0127eb

https://betterprogramming.pub/5-lesser-known-features-of-wkwebview-f20c94998c11

https://www.appsdeveloperblog.com/inject-javascript-into-wkwebview/

https://www.youtube.com/watch?v=JafGypqFvs4

https://stackoverflow.com/questions/48839180/preload-multiple-local-webviews?noredirect=1&lq=1
https://stackoverflow.com/questions/31526819/wkwebview-is-it-possible-to-preload-multiple-urls

https://www.folkstalk.com/2022/10/wkwebview-load-delegate-in-swift-with-code-examples.html

https://stackoverflow.com/questions/49628954/how-to-load-url-on-wkwebview

https://medium.com/capital-one-tech/javascript-manipulation-on-ios-using-webkit-2b1115e7e405

https://medium.com/swlh/web-to-native-code-communication-on-ios-using-wkscriptmessagehandler-8d307b3847fa


## Check WebView loaded

```swift
func webView(_ webView: WKWebView, didCommit navigation: WKNavigation!) {
    print("Start loading")    
}

func webView(_ webView: WKWebView, didFinish navigation: WKNavigation!) {
    print("End loading")
}
```

https://stackoverflow.com/questions/45448443/swift-3-check-if-wkwebview-has-loaded-page



## Clear Cache 

Swift 5 snippet


```swift
WKWebsiteDataStore
.default()
.removeData(ofTypes: [WKWebsiteDataTypeDiskCache,
					  WKWebsiteDataTypeMemoryCache], 
					  modifiedSince: Date(timeIntervalSince1970:0),
					  completionHandler:{ })
```

[Documentation URL](https://developer.apple.com/documentation/webkit/wkwebsitedatastore/1532938-removedata)

https://stackoverflow.com/questions/27105094/how-to-remove-cache-in-wkwebview

## WKWebView Tips


https://github.com/ShingoFukuyama/WKWebViewTips