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

[[config/jailbreak]]

## Certificate

[certificate](certificate.md)

## Provisioning

[provisioning](provisioning.md)


## Secrets
[secret_keys](secret_keys.md)



