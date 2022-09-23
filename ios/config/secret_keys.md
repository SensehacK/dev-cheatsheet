# Secret Keys


You could save your API end point in .plist file which we can specifically ignore committing to the git servers.

Note: If pushing out production App always encrypt out your keys so that decrypting or reverse engineering an app bundle package won’t reveal certain confidential information in the app package.


Make a keys.plist file from Xcode -> File -> New File



## function 

Implement a small function to convert all of your property list keys dictionary format to an object for using it everywhere.

Code to access the keys on app launch.

AppDelegate.swift
```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        
        // Calling the method for converting .plist data to struct object.
        LaunchControl().retrieveKeys()

        return true
    }
```

CustomClass.swift
```swift
import UIKit

struct AppConstants {
    // App Settings
    static var apiHeader = ""
    static var apiKey = ""
    static var baseURL = ""
    
}

class LaunchControl {
    
    func retrieveKeys() {
        if let path = Bundle.main.path(forResource: "Keys", ofType: "plist") {
            
            let keys = NSDictionary(contentsOfFile: path)
            if let apiKey:String = keys?["apiKey"] as? String {
                AppConstants.apiKey = apiKey
            }
       }
    }
}
```


## Git Config

Do configuration of the git locally and make sure you add the “keys.plist” file to .gitignore file. So that it won’t be committed to the repository. 
```gitignore


```
You could share the file to your team members internally or just commit a dummy file name to the repository and stop committing actual values to that file.
   

## Damage control

If you have already committed an API key to git server, make sure you generate a new API key so that they won’t be misused by other developers.
API key and private keys need to be always secret, you could utilize the Github secret keys service to store it on specific platform.

[Github secrets](https://docs.github.com/en/actions/reference/encrypted-secrets)

## Guide

[NS Hipster Secrets guide](https://nshipster.com/secrets/)

## Other Platforms

[React Web app](https://medium.com/better-programming/how-to-hide-your-api-keys-c2b952bc07e6)

