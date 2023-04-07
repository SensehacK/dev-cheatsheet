

## Setup


## Config


## Backup


## Addons

RPC Shutdown

```
service: hassio.addon_stdin
data: 
  addon: core_rpc_shutdown
  input: fluidscape-pc

```

LG Web OS companion

Turn on 
- Source: https://github.com/JPersson77/LGTVCompanion

For C1 and C2 it's All Settings->General->Devices->External Devices->TV On With Mobile->Turn on via Wi-Fi.
Open the administrative interface of your router, and set a static DHCP lease for your WebOS devices, i.e. to ensure that the displays always have the same IP-address on your LAN.


Aprilaire support

Still WIP but no avail yet. Even with Wifi model
I just need the data and logging for pretty charts and monitor how things change for the whole day or every hour or so.

https://community.home-assistant.io/t/aprilaire-thermostat-8800-any-modbus-experts/341414/56


Need to watch this as well
https://www.youtube.com/watch?v=3sRfxc9gBgI

https://www.home-assistant.io/integrations/humidifier.mqtt/

Idea: Maybe tap into aprilaire stats  website or have an android be the mediator between Home Assistant and Aprilaire Thermostat.
Also get values off the data from the app or just get a temperature sensor in the house to monitor full day temps. But that way I won't be able to control the weather from Home Assistant. Maybe have a callback to Google Assistant or Alexa towards making sure sending the weather data or changing temps.
Does it support Air cleaning as well? Don't know.

First thing to do is to add Alexa integration.



## Tuya Smart Life


Creating Dev API account with 1106 Login error

Account ID: 
Tuya app email address

password:
Make sure below 11 chars and no complex symbols $@#!%@

Don't use Tuya IOT Api developer account credentials here.


https://www.reddit.com/r/homeassistant/comments/q3hnlz/tuya_login_error_1106_permission_deny/


Renew my API again for 6 months or restart my Home Assistant to work with Tuya integration.
https://github.com/home-assistant/core/issues/80278

Thread to similar problem of mine.
https://community.home-assistant.io/t/tuya-devices-entities-gone-missing/347445/111
Nov 1st week post by [chrisleeca](https://community.home-assistant.io/u/chrisleeca)[Chris Lee](https://community.home-assistant.io/u/chrisleeca)






## Xcel Smart Energy Meter


I read through the spec and put together the proper commands to generate your own certificate.

```
openssl req -x509 -nodes -newkey ec -pkeyopt ec_paramgen_curve:prime256v1 -keyout key.pem -out cert.pem -sha256 -days 1094 -subj '/CN=MeterReaderHanClient' -addext "certificatePolicies = critical,1.3.6.1.4.1.40732.2.2" -addext "keyUsage = critical,digitalSignature"
```

This will give you `cert.pem` and `key.pem` valid for just under 3 years (which is the maximum valid length).

The LFDI is the first 40 characters of the SHA256 signature.

```
openssl x509 -noout -fingerprint -SHA256 -inform pem -in cert.pem | sed -e 's/://g' -e 's/SHA256 Fingerprint=//g' | cut -c1-40
```

I added this LFDI to my devices in Xcel and the certificates worked a few seconds later.

Currently have it pulling in on my Energy dashboard with:

```yaml
sensor:
  - platform: command_line
    unique_id: xcel_meter_power
    name: "Smart Electric Meter Power"
    command: "/usr/bin/curl --ciphers ECDHE-ECDSA-AES128-CCM8 --insecure --url https://192.168.1.39:8081/upt/1/mr/1/r --cert /config/c.pem --key /config/k.pem 2>&1 | grep -o '<value>.*</value>' | grep -Eo '[0-9]+'"
    unit_of_measurement: "W"
#    device_class: 'power'
    scan_interval: 5
    command_timeout: 5

  - platform: command_line
    unique_id: xcel_meter_consumption
    name: "Smart Electric Meter Consumption"
    command: "/usr/bin/curl --ciphers ECDHE-ECDSA-AES128-CCM8 --insecure --url https://192.168.1.39:8081/upt/1/mr/3/r --cert /config/c.pem --key /config/k.pem 2>&1 | grep -o '<value>.*</value>' | grep -Eo '[0-9]+'"
    unit_of_measurement: "kWh"
    value_template: "{{ value | multiply(0.001) | round(3)}}"
#    device_class: 'energy'
#    state_class: 'total_increasing'
    scan_interval: 5
    command_timeout: 5

homeassistant:
  customize:
    sensor.smart_electric_meter_consumption:
      device_class: energy
      state_class: total_increasing
    sensor.smart_electric_meter_power:
      device_class: power
      state_class: measurement
```


```bash
curl --ciphers ECDHE-ECDSA-AES128-CCM8 --insecure -v --url https://192.168.0.80:8081/upt --cert /config/otherxcelcerts/cert.pem --key /config/otherxcelcerts/key.pem

curl --ciphers ECDHE-ECDSA-AES128-CCM8 --insecure -v --url https://192.168.0.80:8081/upt --cert /config/xcelcerts/cert.pem --key /config/xcelcerts/key.pem
```