
# Security 

## Description

Security is one of those things you would have to consider with iOS product app lifecycle.
Thankfully Apple does the heavy lifting most of the times and the end user can rest assure that the app they have installed follows certain security requirements from industry standards.


## Check ATS report


```bash
nscurl --ats-diagnostics <URL here> --verbose
```

## App Transport Plist

[ats_plist](ats_plist.md)


## Sideloading
You would need a jailbreak or some kind of developer account access inorder to side load apps via signing them with your developer account. Apple usually requires you to run signed code on iOS ecosystem. On macOs it will give the warning of `Unverified developer / App` but on iOS it won't let you install the app. You could circumvent that requirement by jailbreaking / rooting your iPhone to run unsign code / app on your physical device.

[[third_party_apps]]

## Certificate

[certificate](certificate.md)

## Provisioning

[provisioning](provisioning.md)

## Code Signing

[framework](/ios/library/framework#Code%20Signing%20XcFramework)

## Secrets
[secret_keys](secret_keys.md)



## Proxy

Using [charles_proxy](charles_proxy.md) or [proxyman](proxyman.md) for capturing traffic via `man in the middle` attack.

SSL Pinning

[Proxyman | Can we bypass SSL Pinning?](https://proxyman.io/posts/2019-11-15-Can-we-bypass-ssl-pinning)


[Great insight from MiTM on iOS vs android here](https://github.com/AlexTech01/Authy-iOS-MiTM?tab=readme-ov-file#compatibility-note)

This method will never work on unrooted Android devices due to the fact that the Authy app only trusts root certificates from the system store and rooting being needed to add certificates to the system store. If you have a rooted Android device and would like to use this guide, add the mitmproxy certificate to the system store instead, and you should be able to follow this guide normally. The reason this works on iOS is that iOS treats system root CAs and user-installed root CAs the same by default, and unless an app uses SSL pinning or some other method to deny user-installed root CAs, it can be HTTPS intercepted via a MiTM attack without a jailbreak needed. If Twilio wants to patch this by implementing SSL pinning, they absolutely can.

## Code Scanning tools


[mend](https://www.mend.io/)

[swift support from mend tool](https://docs.mend.io/bundle/mend_sast/page/swift.html#Mend-SAST-supported-Swift-frameworks)

[github action support](https://github.com/whitesource/GitHubPackagesSecurityAction)

[Common Weakness Enumeration (CWE)](https://cwe.mitre.org/index.html)



## Security SDK

[zimperium](https://www.zimperium.com/platform/) Use this for threat modeling and checking what's going on device. It's kinda anti tamper / root detection system in place. Don't know if its that useful for anti tamper.

[zimperium | mobile app protection suite](https://www.zimperium.com/mobile-app-protection/)

Tbh I don't think you need anti tampering sdk on your platform but sometimes the business has weird recommendation in order to be compliant with the law or get some better score on some bureaucracy report shared to its stakeholders or its a contractual obligatory agreement in order to hand over some copyrighted material in a form of digital medium.

I have the opinion that no matter how good the security is, hackers will still be able to get away with it. Its just a matter of do they deem necessary to take a "crack" at your product (pun intended) or do they get any monetary or street cred by breaking your security. All we can do is slow the progress or make our product not enticing enough that they prefer this cat and mouse game. 

Heck if [Denuvo](https://en.wikipedia.org/wiki/Denuvo) can be crack, you betcha your mediocre product would be as well. [piracy](/thoughts/piracy.md)


[Check out Tampering detection](/ios/config/resigning#Jailbreak%20or%20Tampering%20detection)
