

## Mind Map

[Video Terms | Ads](architecture/terminologies/video_terms#Ads)

## Google Ads

For iOS to include ads in Xcode, apple ecosystem with Google backend DAI.
[Interactive Media Ads SDK](https://developers.google.com/interactive-media-ads/docs/sdks/ios/client-side)

## VAST

[source | iab tech lab](https://iabtechlab.com/standards/vast/)

VAST ([Video Ad Serving Template](https://www.google.com/search?newwindow=1&client=firefox-b-1-d&sca_esv=c968e65ff83469d2&cs=1&q=Video+Ad+Serving+Template&sa=X&ved=2ahUKEwiyo9q1wvaNAxXvJzQIHQKvKZIQxccNegQIAhAB&mstk=AUtExfDfZvpE0HhPAaRpgVPRtX1-k8a1uafhsh8Ps_m37_AUr6hEqP-uvZyTGCpF5XoiMgY_HdGhQDQLKZH8rU1ovgUnW_sjniPwir_7OHucx9ykWAUdasDrfvlEZCoUsvbXeAcq93hBit1OxGkQUlaEdSeIh7TIdsm3RGsfjOea7uW5qam8a1BcByBxtB-0O6gOc_ff&csui=3)) is a standard for delivering video ads, and IMA ([Interactive Media Ads](https://www.google.com/search?newwindow=1&client=firefox-b-1-d&sca_esv=c968e65ff83469d2&cs=1&q=Interactive+Media+Ads&sa=X&ved=2ahUKEwiyo9q1wvaNAxXvJzQIHQKvKZIQxccNegQIAhAC&mstk=AUtExfDfZvpE0HhPAaRpgVPRtX1-k8a1uafhsh8Ps_m37_AUr6hEqP-uvZyTGCpF5XoiMgY_HdGhQDQLKZH8rU1ovgUnW_sjniPwir_7OHucx9ykWAUdasDrfvlEZCoUsvbXeAcq93hBit1OxGkQUlaEdSeIh7TIdsm3RGsfjOea7uW5qam8a1BcByBxtB-0O6gOc_ff&csui=3)) is Google's SDK that helps publishers integrate these ads into their content.



**VAST:** A standardized XML schema for delivering video ads, allowing for consistent ad serving across different platforms and players. 

- **IMA:** Google's SDK that simplifies the process of integrating video ads into websites and apps. 

- **Client-side vs. Dynamic Ad Insertion (DAI):** IMA supports both client-side integration (where ads and content are combined within the app) and DAI (where ads and content are combined on the server side). 

- **Companion Ads:** Ads displayed alongside the main video ad, often in HTML format. 

- **IDFA/ADID:** Identifiers used for targeted advertising on mobile devices


[VAST vs VPAID](https://www.exads.com/blog/how-to-use-vast-vpaid-vmap-and-vast-waterfall)

[VAST Wiki](https://en.wikipedia.org/wiki/Video_Ad_Serving_Template)



## SCTE 

SCTE 35 Signalling

### Tools

decrypt / decode

base64 bit mapping of SCTE Binary ( CUE = value)

```ts
#EXT-X-SCTE35:TYPE=0x34,CUE=/DBbAAFFsYloAP/wBQb+kyuKZgBFAAhDVUVJAAAAAAI5Q1VFSQAABr9/2wABqbhgASM2YzkyZWRiLTVmNmUtNDdiNC05ZjE3LWIzOTljYTI4YjAxZDQAAAEBeJ8OvA==,ELAPSED=0.000
```

[scte35-js | comcast SCTE parser tool](https://comcast.github.io/scte35-js/)

Input: `/DBbAAFFsYloAP/wBQb+kyuKZgBFAAhDVUVJAAAAAAI5Q1VFSQAABr9/2wABqbhgASM2YzkyZWRiLTVmNmUtNDdiNC05ZjE3LWIzOTljYTI4YjAxZDQAAAEBeJ8OvA==`

Output: 

```json
tableId: 252
selectionSyntaxIndicator: false
privateIndicator: false
sectionLength: 91
protocolVersion: 0
encryptedPacket: false
encryptedAlgorithm: 0
ptsAdjustment: 5466918095
cwIndex: 0
tier: 4095
spliceCommandLength: 5
spliceCommandType: 6
spliceCommand: Object {"specified":true,"pts":3460017948}
descriptorLoopLength: 69
descriptors: Array[2] [{"spliceDescriptorTag":0,"descriptorLength":8,"identifier":"CUEI"},{"spliceDescriptorTag":2,"descriptorLength":57,"identifier":"CUEI","segmentationEventId":1739,"segmentationEventCancelIndicator":false,"programSegmentationFlag":true,"segmentationDurationFlag":true,"deliveryNotRestrictedFlag":false,"webDeliveryAllowedFlag":true,"noRegionalBlackoutFlag":true,"archiveAllowedFlag":false,"deviceRestrictions":3,"segmentationDuration":27900000,"segmentationUpidType":1,"segmentationUpidLength":35,"segmentationUpid":{"0":54,"1":99,"2":57,"3":50,"4":101,"5":100,"6":98,"7":45,"8":53,"9":102,"10":54,"11":101,"12":45,"13":52,"14":55,"15":98,"16":52,"17":45,"18":57,"19":102,"20":49,"21":55,"22":45,"23":98,"24":51,"25":57,"26":57,"27":99,"28":97,"29":50,"30":56,"31":98,"32":48,"33":49,"34":100},"segmentationTypeId":52,"segmentNum":0,"segmentsExpected":0,"subSegmentNum":1,"subSegmentsExpected":1}]
crc: 4033749405
```


[tsDuck](https://tsduck.io/)
The free and open-source reference framework for MPEG transport streams


## Quartiles



How Ad Quartiles are Determined

Ad quartiles measure **viewability and completion rates**, not a statistical ranking of ad quality. The four quartiles are: 

- **First Quartile (Q1):** The ad has played for at least 25% of its total duration.
- **Midpoint (Q2):** The ad has played for at least 50% of its total duration.
- **Third Quartile (Q3):** The ad has played for at least 75% of its total duration.
- **Complete:** The ad has played to 100% completion. 

The tracking system (either server-side or client-side) is responsible for sending a beacon to the ad server each time one of these milestones is reached.


[SO | swift proper way to measure time](https://stackoverflow.com/questions/47850390/proper-way-to-measure-time-in-swift)
