# User Notifications



## Push Notifications

Open app in specific view when push notification is tapped
https://fluffy.es/open-specific-view-push-notification-tapped/


Best Practices around Notifications
https://blog.hurree.co/ios-push-notification-permissions-best-practises
https://tanaschita.com/20220502-quick-guide-on-local-notifications-for-ios/



## Simulate Push notification in Simulator

Create `custom_notification.apns` file with your target identifier.
```text
{
	"Simulator Target Bundle": "com.your.targets.bundle.identifier",
	"aps": {
		"alert": "Push Notifications Test",
		"sound": "default",
		"badge": 1
	}
}
```

Drag and drop the file in iOS / iPadOS simulator. As long as the app bundle ID is correct and the simulator has the app installed it should show the right notification.

You need to have asked a permission for allowing notifications on the app you want to test push notifications.

SwiftUI notifications permission

```swift
VStack {
	Text("Hello Kautilya!")
}
.onAppear {
	UNUserNotificationCenter.current().requestAuthorization(options: [.badge, .sound, .alert]) { _, _ in 
		print("Hello Again?")
	}
}

```


Generate a `.pem` file for notifications apns authentications
https://developer.blueshift.com/docs/generate-a-pem-file

## Local Notifications



## References

https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/generating_a_remote_notification

