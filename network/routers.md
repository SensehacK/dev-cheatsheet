# Routers

## Intro

- WiFi -> Wireless Fidelity

## Notes

- Always mention it as Access Points not a Wifi router
- 

## Two types of Access points

###  Home / Personal
- Arris
- Tplink
- Netgear

### Enterprise

- Cisco
- Rukus
- Extreme
- Aruba
- CMBian

## [Network Testing](network_testing.md)


## [Project Management](project_management.md)




## History

- We moved from Ethernet -> Wifi
- Move around - seamless connectivity
- Security aspect - wifi sniffing - catching the packets.



## [router_security](router_security.md)



## Terminologies

### SSID
The name of the AP Identifier.

## 2.4 Ghz

- Non overlapping channels
- What channels AP shouldn't be using
- What DFS channels are using
- 20 mhz how many channels:?
- In 40 mhz how many channels
- 11 channels I believe in 2.4ghz
- 1 , 6 and 11 are loosely coupled with least interference. 
- Better coverage
- Penetrates better through solid files
- It is legacy and more optimized overall.
- Enterprise AP connected Wifi routers 2.4 ghz is more suitable.

## 5 Ghz
- Lower coverage
- Faster transfer rates
- Can penetrate lesser
- Suited for 4K or higher bit rate content. 
- Newer technology

####  Wifi 6 ax

#### Wifi 6E


## Wifi 7


## 6 hz


## RF

### 80 11



### Radio Patterns

- two or three patterns
- 22 mhz channel range usual range.
- Auto setting to select specific channels most of the time on router admin page.

### Exempted Frequencies

- Also certain radio frequencies are always restricted for Federal for aviation and other security stuff.
- 

### Site Surveys

- How the AP are deployed
- Signal strength - Heat Map
- Channels in the picture - picking the right auto channel.

### Collision Detection / Avoidance


## Radio Frequency Isolation

- RF Boxes 
	- Antennas from one box to another chamber box. For isolated tests

- RF Chamber
	- Laptop can take control of doing speed tests, channels to access outside the chamber
	- External AP access, without being in the chamber. Security, throughput, channel width
	- Present onsite in a lab for testing.

- Screen rooms

- Brands 
	- Ramsey shield box RF shield box.




## Debug

- Verbose Wifi SSID logging
- Turn on verbose logging through Android system settings.
- AP would show little bit slower because it may not have updated reactive web UI.





## Beacons
- Listening to beacons is part of passive scanning


## Timeline

- Wifi client -> Wifi AP
Active Scanning

Authentication handshake
- Probe request <->  Ack
- Authentication Request  <-> Ack
- Association Request <-> Ack



## [DHCP](DHCP.md)

## Difference

- Active vs Passive Scanning


## [Switch](network/switch.md)

## Interview

- Diff between active and passive scanning with examples