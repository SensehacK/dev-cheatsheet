
## Android 15

> AI copied

To set up Charles Proxy on an Android 15 device, you'll need to configure both your computer's Charles Proxy application and your Android device's network settings. This involves enabling SSL proxying in Charles, configuring your Android device to use a proxy, and installing the Charles root certificate on your device. 
1. Configure Charles Proxy on your Computer:

    Enable SSL Proxying:
    . 

In Charles, go to Proxy > SSL Proxying Settings and enable the "Enable SSL Proxying" checkbox. Add the specific domains you want to proxy by clicking "Add" and entering the host name and port. 
Save Charles Root Certificate:
.
Go to Help > SSL Proxying > Save Charles Root Certificate and save it in a location you can easily access. 

2. Configure Proxy Settings on your Android Device:

    Connect to Wi-Fi:
    Ensure your Android device is connected to the same Wi-Fi network as your computer. 

Set up Manual Proxy:
Go to Settings > Network & Internet > Wi-Fi > (selected network) > Modify Network > Advanced options. Select Manual for the proxy type, enter your computer's IP address as the proxy hostname, and 8888 as the port. 
Install Charles Root Certificate:

    Open a web browser on your Android device and go to http://charlesproxy.com/getssl. 

Download the Charles root certificate. 
Go to Settings > Security > Encryption & credentials > Install from storage and select the downloaded certificate file. 
Name the certificate and verify that it's listed under Trusted credentials. 

3. Configure your Android app (if needed):

    If you're using an app you control, you may need to add a network security configuration file to your app to trust the Charles root certificate. This allows the app to trust certificates that Charles generates. 

This video demonstrates how to set up Charles Proxy with an Android phone:


## References

[charles setup guide](https://docs.tealium.com/platforms/android-kotlin/charles-proxy-android/)

