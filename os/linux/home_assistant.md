

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
