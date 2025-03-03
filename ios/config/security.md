
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

## Code Scanning tools


[mend](https://www.mend.io/)

[swift support from mend tool](https://docs.mend.io/bundle/mend_sast/page/swift.html#Mend-SAST-supported-Swift-frameworks)

[github action support](https://github.com/whitesource/GitHubPackagesSecurityAction)

[Common Weakness Enumeration (CWE)](https://cwe.mitre.org/index.html)

