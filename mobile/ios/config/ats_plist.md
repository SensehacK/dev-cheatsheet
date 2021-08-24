App Transport Security Plist


## Unsecure HTTP Network Calls


In Xcode, Apple has enforced developers to adapt Https network calls and if you still want to rely on unsecure http protocol for your network calls.
You would need to set a certain flag in Info plist file to allow arbitrary loads or specific domain loads.

From security standpoint, the app developer should always only allow certain domain names to be accessible using http for greater security and data transmission.

```xml
<dict>
	<key>NSAppTransportSecurity</key>
	<dict>
		<key>NSExceptionDomains</key>
		<dict>
			<key>herokuapp.com</key>
			<dict>
                <key>NSExceptionAllowsInsecureHTTPLoads</key>
                <true/>
                <key>NSIncludesSubdomains</key>
                <true/>
            </dict>
		</dict>
	</dict>
</dict>
```

[SO](https://stackoverflow.com/questions/32892121/xcode-7-1-beta-2-disable-ats/32894812#32894812)
