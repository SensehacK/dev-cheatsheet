

## Encryption Compliance


This screenshot shows the random popup question for compliance.
Best advice is usually consult with your product legal team. 
But we can usually get away with `Standard encryption` settings since if you're accessing `Keychain` or `CryptoKit` library or anything to do basic encryption / decryption of data being transferred from your app to backend server. You would have to be upfront about this information in order to reflect the app review process easily. As well as certain countries like France would make it mandatory to have a compliance document for any app being able to be accessed from a specific region.

Of course none of this is any legal advice & my only advice would be to consult technology legal laws or Lawyers or attorneys or whatever legal body they are being represented as.



![](export_compliance_missing.png)



## Rollout


Phased Rollout

Notes from App Store Connect
### Phased Release for Automatic Updates: Paused at Day N

Phased release for automatic updates lets you gradually release this update over a 7-day period to users who have turned on automatic updates. Keep in mind that this version will still be available to all users as a manual update from the App Store. You can pause the phased release for up to 30 days or release this update to all users at any time. [Learn More](https://developer.apple.com/help/app-store-connect/update-your-app/release-a-version-update-in-phases)

It is usually a good idea to pause a rollout if something goes wrong on production.
We don't have the option to rollback a release on ASC. So only way to do a rollback is submit a new version - hotfix after the previous version is set to 100% rollout and then quickly send a new build to ASC to override it with your rolled back app package from previous tags.


Release strategy about ASC rollout & rollbacks.
https://www.gabrielle-earnshaw.com/posts/phased-releases-for-ios-apps-on-app-store-connect/


Big Bang Release Case 
https://www.gabrielle-earnshaw.com/posts/mitigating-the-risk-of-big-bang-app-releases/