# Video Terms

## Intro

So while being in high level architecture meetings around working in video streaming space, I quickly realize the exorbitant amount of acronyms used daily in those conversations. So I decided to expand upon my learnings and categorized them so that its easier for me to refer or forward my learnings to someone in need.


## Media 

Info copied from [whatwg.org](https://html.spec.whatwg.org/multipage/media.html#media-resource)
### Media Resource

A [media resource](https://html.spec.whatwg.org/multipage/media.html#media-resource) has an associated origin, which is either "`none`", "`multiple`", "`rewritten`", or an [origin](https://html.spec.whatwg.org/multipage/browsers.html#concept-origin). It is initially set to "`none`".

A [media resource](https://html.spec.whatwg.org/multipage/media.html#media-resource) can have multiple audio and video tracks. For the purposes of a [media element](https://html.spec.whatwg.org/multipage/media.html#media-element), the video data of the [media resource](https://html.spec.whatwg.org/multipage/media.html#media-resource) is only that of the currently selected track (if any) as given by the element's `[videoTracks](https://html.spec.whatwg.org/multipage/media.html#dom-media-videotracks)` attribute when the [event loop](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop) last reached [step 1](https://html.spec.whatwg.org/multipage/webappapis.html#step1), and the audio data of the [media resource](https://html.spec.whatwg.org/multipage/media.html#media-resource) is the result of mixing all the currently enabled tracks (if any) given by the element's `[audioTracks](https://html.spec.whatwg.org/multipage/media.html#dom-media-audiotracks)` attribute when the [event loop](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop) last reached [step 1](https://html.spec.whatwg.org/multipage/webappapis.html#step1).

### Media Element

[Media elements](https://html.spec.whatwg.org/multipage/media.html#media-element) are used to present audio data, or video and audio data, to the user. This is referred to as media data in this section, since this section applies equally to [media elements](https://html.spec.whatwg.org/multipage/media.html#media-element) for audio or for video. The term media resource is used to refer to the complete set of media data, e.g. the complete video file, or complete audio file.



## Video

### Main Video


### SDR

Standard Dynamic Range


### HDR

High Dynamic Range

#### HDR 10

#### Dolby Vision

#### HDR - Extended


### BitRate

The content being encoded with given bits for every scene / every second.

eg. 200 MB file of resolution 1080p (full HD) (16:9 aspect ratio) of 10 mins with x265 (HEVC) encoding has a suggested average of `3728.75` kbps according to this calculator. Of course it depends on what content is being played and the scenes in the video.

check out video bitrate calculator in [tools section](tools/apps#Calculators)


### Resolution

#### HD

High Definition

720p - HD
1080p - FullHD 
2160p - UItraHD


#### SD

Standard Definition

360p
480p
560p




### Aspect Ratio

16:9 - common Widescreen ( HDTV ) (720p, 1080p , 2160p)
16:10 - Laptop Widescreen sometimes.
21:9 - Ultra wide
4:3 - CRT TV (Old TVs) Old Nintendo / console games

2.39:1 - widescreen cinema

### Letterboxing

letterboxing (‘black bars’) in the video
## Text
### Subtitles

The term "subtitles" is used for transcriptions of spoken text providing translations in different languages for viewers.

**Subtitles** are a form of captioning used to translate the audio dialogue from one language into another. Simply put, subtitles translate a video’s language into another. You’ll see subtitles used in many foreign films and programs.

[beginners guide for subtitles](https://www.xl8.ai/blog/the-beginners-guide-for-subtitle-format-users)

### Closed Captions

Closed captions are created to **allow people who are** **deaf or hard of hearing to experience the video**, so they also include background sounds and speaker changes. On the other hand, subtitles assume that the viewer can hear the audio and as a result do not contain the background sounds or notifications for speaker changes.

[What is 608 and 708 Closed Captioning?](https://www.3playmedia.com/blog/difference-cea-608-cea-708-captions/)



### Hard vs Soft

"Soft" subtitles (which can be toggled on and off) are supported by the WebVTT standard in a similar fashion to captions (they've both categorized as timed metadata);

if you preferred "hard" subtitles (where they are "burned" into the video), you would provide the subtitle data to your video encoder during the transcoding process.


## Audio

### Normal Audio

### Commentary

### Dub


### Stereo

Left and Right channels in the audio stream. Hence Stereo

### Mono

Only one directional sound pumped in or recorded.

### Surround

Has L + R, Back L + R, Subwoofer and Center.
5.1
5 Channels and .1 is the subwoofer

7.1 
7 channels and 1 subwoofer

7.2.4
7 channels, 2 subwoofer and 4 height ceiling speakers

### Spatial Audio

Doesn't only have L + R channels but it has more channels to support Height information as well.
Apple has its own variant of Dolby Atmos kind of implementation.
Windows has Spatial audio surround.
Apple Airpods support spatial audio with extra meta data of input source file and use headphones accelerators hardware sensors to map it to surround sound.



### Audio ducking

Audio ducking is a technique where the volume of one audio signal (the "ducked" signal) is temporarily lowered when another audio signal (the "ducking" signal) is present, often used to improve clarity and intelligibility, especially when mixing music with narration or other audio.


## Ads

### Pre Roll | Mid Roll | Post Roll

Pre roll just means ads that are played before content playback begins.
Mid Roll would be an ad being played in middle.
Post Roll ad at the end.

### Quartile

First Quartile | Second (Median) | Third Quartile
Q1 | Q2 (Mid) | Q3

25% | 50% | 75%


[quartile formula](https://www.cuemath.com/quartile-formula/)

```js
export type QuartileType = "First" | "Second" | "Third" | "Last";
```

### Ad Break

An ad content which has duration of time to be played with resolution and links.


### Ad Schedule

Collection | Array of Ad Breaks in a video stream file.



### DAI

Dynamic Ad Insertion


### Freewheel 

Ad server which you can plug in - whose sole responsibility is to give us an array of ads "personalized" ads depending on the user being fingerprinted at the current instance.

### Server Side Ads

SSAI 
Server Side Ad Insertion

### Segment

I don't know what is a segment

### SCTE - 35

Scete tag to find the information around HLS / stream.
Convey information 

> This standard, “Digital Program Insertion Cueing Message for Cable” (SCTE 35), is the core signaling standard for advertising, Program and distribution control (e.g., blackouts) of content for content providers and content distributors. SCTE 35 is being applied to QAM/IP, Title VI/TVE (TV Everywhere), and live/time shifted (DVR, VOD, etc.) delivery. SCTE 35 signals can be used to identify advertising Breaks, advertising content, and programming content (e.g., specific Programs and Chapters within a Program).

[Message cues embedded in content manifests.](https://www.scte.org/standards/library/catalog/scte-35-digital-program-insertion-cueing-message/)

#### AI Overview

SCTE-35 tags are used in HTTP Live Streaming (HLS) to indicate ad breaks, content transitions, and other program information: 

- **Ad breaks**: SCTE-35 tags signal when ads should be inserted into the stream. 

- **Content transitions**: SCTE-35 tags indicate when content should be switched within the stream. 

- **Program information**: SCTE-35 tags can indicate program information such as intro/outro credits, chapters, blackouts, and extensions. 

- **Blackouts**: SCTE-35 tags can signal when a piece of content should be replaced or omitted from a broadcast. 

SCTE-35 tags are visible in the .m3u8 manifests of HLS. Some examples of SCTE-35 tags include: 

- **#EXT-X-CUE-OUT**: Indicates the start of an ad insertion or splicing event.
- **#EXT-X-CUE-IN**: Indicates the conclusion of an ad insertion or splice event.
- **OATCLS-SCTE35**: Contains the base64 encoded raw bytes of the original SCTE-35 advertising available message.
- **EXT-X-DATERANGE**: Uses UTC to rely on timing.

SCTE-35 markers can be included in transport stream (TS), DASH, HLS, and CMAF outputs.


```ts
#EXT-X-SCTE35:TYPE=0x41,CUE=/DB7AAAAAAAAAP/wBQb+sPKHTfsn+XAABBAACRCZCg///////
```

[Ref | Bitmovin | SCTE-35 guide](https://bitmovin.com/blog/scte-35-guide/)

[scte parser | online tool](https://tools.middleman.tv/scte35-parser)

## HLS 

Apple's implementation of delivering video content via internet HTTP Live Streaming format specification.
Android / Roku and other platforms use DASH instead of HLS.
This HLS file is also sometimes referred as manifest file.

`.m3u8` file format in Text readable format.

## [HLS Format Examples](HLS_types.md)

## Assets

There are many different asset types in video streaming. 
OOH - Out of Home
**TVE**  - TV Everywhere
m3u8 manifest on iOS and .mpd on Android. .mp4 fragments

### VOD

Video on demand

Ads aren't valuable for first few days
C3 for VOD is not that valuable like Linear Live TV.

C3 
C4  - Day four


### IVOD

IVOD	Impulse Video on Demand
IVOD	Internet Video on Demand
IVOD	Interactive Video On Demand
IVOD    Instant Video On Demand

IVOD - Instant content on demand. Usually a few seconds behind T6 Linear broadcast. 


### TVE VOD

Content on demand available OOH  

### Linear

Also referred as `TVE Linear` or `Live TV`

[what is linear tv](https://target-video.com/what-is-linear-tv/)

### Live Asset

### T6 Title 6 

Basically just rules from USA govt. to make sure they comply with certain rules
Title 6 or Title VI – Cable television service, which is governed by Title VI of the Communications Act.

[what-title-6-video](https://www.nexttv.com/news/what-title-6-video-381860)

### T6 LINEAR

Live content NOT available OOH  

### T6 VOD

Content on demand NOT available OOH  

### T6 VOD Server Side Ads

A special fallback protocol exists for T6 VOD assets which inserts ads from server side. It kinda manipulates manifest. Internally its codenamed as VEX.



### Other

PURCHASE - These are assets that the user pays to watch.  
RECORDING - User recorded content. Can be watched in home or non home locations



## Time 

### Wall Clock

Actual UTZ time with full format - Date and Time.


### Offset Time

`TimeMSec` - Milli Secs
Or an offset of Secs from the initial playback stream head.


### Unix Epoch 

Its a unix date time variant to describe a constant way of time format.

### Time Scale


90k or 100k
30fps 
24 fps it all divides evenly in 90k
60fps

### PTS 

Presentation timestamp
The presentation timestamp (_PTS_) is a timestamp metadata field in an MPEG transport stream or MPEG program stream that is used to achieve synchronization of programs' separate elementary streams (for example Video, Audio, Subtitles) when presented to the viewer.
[PTS Wiki](https://en.wikipedia.org/wiki/Presentation_timestamp)

## Formats

### MPEG

### AAC

### HEVC

It has both hvc1 and hev1 formats

> hvc1 parameter sets are stored out-of-band in the sample entry (i.e. below the Sample Description Box ( stsd ) box)

> hev1 parameter sets are stored out-of-band in the sample entry and/or in-band in the samples (i.e. SPS/PPS/VPS NAL units in the bitstream/ mdat box)

[comment source](https://community.bitmovin.com/t/whats-the-difference-between-hvc1-and-hev1-hevc-codec-tags-for-fmp4/101)


### AV1




## Encoders

[video encoding tips](https://www.dr-lex.be/info-stuff/videotips.html)

### Packager 

Super 8 - Internal tool to package streams via Just in time to deliver right encoded assets from different tools.

## Decoders


### O&O

Owned and Operated channels. Generally 3rd party channels with their own encoder/decoder - packaging the whole nine yards of delivering their IPs.

## Broadcasting

### EAS

Emergency Alert System - this is being used for broadcasting emergency video over television or network to provide shelter / tornado / war anything which takes precedence since it could be life threatening. I don't have any examples since I haven't had the chance to watch live tv too much in north america. But I'm guessing this would have been placed by broadcasting FCC or governing agency after world war II or cold war to quickly mitigate broadcast messages or sirens like the ole' days of radio broadcast interrupt as depicted in ["Tom & Jerry" show.](https://youtu.be/a3-Glb0Y3Jg?si=jA6DRhu3vQDWYRna)

[FCC | fema - EAS](https://www.fema.gov/emergency-managers/practitioners/integrated-public-alert-warning-system/public/emergency-alert-system)


## Streaming

### IP Video

IP Video is **a term used to describe video that is distributed on an IP network**. The “IP” in IP Video stands for Internet Protocol, which is a set of standards for communicating over computer networks. IP Video devices can include cameras, hardware or software switchers, graphic workstations, and displays.
[Source](https://streamgeeks.us/what-is-ip-video/)

### OTT

Over the top

OTT, short for "Over-the-Top," refers to the delivery of video and audio content over the internet, bypassing traditional broadcast or cable providers. This includes services like Netflix, Amazon Prime Video, and Hulu, where users can access content through apps or websites on various devices


## Unique Tags
### SCTE 

Scete tag to find the information around HLS / stream.
Convey information 

```ts
#EXT-X-SCTE35:TYPE=0x41,CUE=/DB7AAAAAAAAAP/wBQb+sPKHTfsn+XAABBAACRCZCg///////
```




## Time Shifting

[Wiki - time shifting](https://en.wikipedia.org/wiki/Time_shifting)

In broadcasting, **time shifting** is the recording of programming to a storage medium to be viewed or listened to after the live broadcasting.


### DVR

Digital Video Recorder - [Wiki](https://en.wikipedia.org/wiki/Digital_video_recorder)

### VCR 

[wiki - video cassette recorder](https://en.wikipedia.org/wiki/Video_cassette_recorder) 

### CDVR

cloud DVR

[CDVR FAQs by Spectrum](https://www.spectrum.net/support/tv/cdvr-faq)
Recording (can be for TVE or T6)


### TSB

Time shift buffer

#### CTSB

Cloud time shift buffer

[time shift tv explained](https://www.edgeware.tv/product/time-shift-tv/)

### FOG

FOG - Fetches live linear manifest and fragment from TSB as if it is from cloud.

Internal tooling to host a local web server using mongoose to serve video/audio content from its local or cloud recorded state. It is a proxy implementation to make sure that the SDK interface remains similar like its interacting with an actual network URL. Instead of using DASH | HLS manifest file url endpoints it proactively proxies them to redirect towards cloud | local recording assets.
Pretty neat, I think we do this in-order to avoid some restrictions on certain DRM streams etc. Not fully known why this workaround is being put in place by certain video streaming libraries or products.


### Recording
#### Hot Recording 

The timeline keeps playing while recording?
When the recording is happening in work in progress and still Live playlist.
The playlist "Event" style playlist (Hybrid of Linear and VOD).
It just starts with `n` number of fragments and it keeps adding more fragments on apple HLS.

#### Cold Recording

When the recording is completed and then it becomes cold recording.
The playlist will become VOD playlist.


## Guides

### EPG

[electronic program guide](https://en.wikipedia.org/wiki/Electronic_program_guide) (EPG)

Interactive programming guides (IPGs)
Or TV Listings | TV guides


###  Channel Surfing

When you watch channels quickly going back and forth with other cable channels to see if something interesting is going on.

[wiki](https://en.wikipedia.org/wiki/Channel_surfing)


## Session

### Heartbeat 

As described by my architect.
It's generally a periodic request sent as a 'keep alive' / I'm still here / periodic update mechanism. Like the player sending a heartbeat analytics message every 60s with info about the stream. The app also sends a periodic request to monitor that the user is still watching a stream and count towards their max concurrent streams limit.

Could be also extended towards the Analytics heartbeats.


## CDN 

### Client Steering

HLS Content Steering | apple specific
[apple wwdc | Deliver reliable streams with HLS Content Steering](https://developer.apple.com/videos/play/wwdc2022/10144/)


[Tech Papers: Implementing HLS/DASH Content Steering at Scale](https://www.ibc.org/technical-papers/ibc2023-tech-papers-implementing-hls/dash-content-steering-at-scale/10258.article)


### URL Reform

This is where the new URL's are generated according to different CDN and replace the regex accordingly.



## URL

We kinda follow a RFC for decoding the URL asset resource to hit the asset resource `n` times depending on the `retry` strategy or different CDNs.

### URL Resolver

### URL Parser


See brand specific Sky implementation product name `Conviva` 



## Upscaling 

### Soap Opera effect

Frame insertion / intermission / adding 
Interpolating
24 fps -> 60 fps


DSP (Digital Signal Processing)


## Analytics

### Nielsen

The company to catch audience viewing measurement analytics by actual hardware in live tv.

### VPA

Internal Platform Analytics which plugs in the data depending on the object file defined for us.


### Open Measurement

Its like an ad measurement analytics service like Nielsen. But for ads - verification.

[open measurement sdk](https://iabtechlab.com/standards/open-measurement-sdk/)



## Previews

### Thumbnail generation


You can do it via i-frame or something in the HLS manifest file



## Playback
### Trick Play

When you disable the fast forward or rewind on the player controller in the video. When you disable / enable the trick play - it gives the user an option to get full control of the scrubbing or jumping on the timeline ++ / -- .
Seeking operations on the timeline.

### Timeline

Its the progress bar on the video player.
Showcasing how much progress it has made eg. 2 mins video
35 secs have passed 

```sh
// - for the video playback
// = for time passed
= = = = - - - - - - - - - - - - - - - - - - - - - - - - - -

// * for ads
* * = = = - - - - - - - - * * * - - - - - - - - - - - * * * -
```

but its not purely for ads as you think of them, they could have a bumper for another program before or after the content with this API like for live tv programming.

### Retune

When the player needs to be deallocated and then retuned or restarted from scratch in order to initiate the state properly. Reset basically.

## [DRM](/ios/media/DRM.md)

Digital Rights Management

### Hardware

### Software

### Widewine


### Fairplay

Apple's variant of DRM on audio / video. HLS and AV Foundation | AVKit libraries.
[fairplay](ios/media/airplay.md)


## Brands

### Sky

Sky is an european video giant for publishing video

Sky Go
Sky EPG

Tata Sky - joint venture with Tata (India) & Sky

 
#### Conviva

I believe this is just a product name for Sky (Europe) which does the URL parsing and resolving.
CDN steering and analytics module for Video streaming.

### Xfinity 

Comcast brand for internet and entertainment brand.

Peacock
Xfinity Stream - Cable subscribers app for streaming video on their mobile devices.


### Netflix


### Google 

Youtube

Youtube TV
Play Music
Youtube Originals



### Disney

Disney Plus
ESPN


### Paramount

Paramount Plus



### Warner Bros

Discovery




## Hardware

### TV

Television


### CTV

Connected TV

### LG

Life's Good


## Software

### webOS

Palm webOS, which was bought by HP (Hewlett Packard) and then LG bought it for their CTV OS. First webOS tv, I believe in 2013 - 14. I used to love my first webOS tv from LG. Multitasking and what not.

### Fusion Player

Seems like something internally used at comcast for web js player.


## Reference

[Closed Captions vs Subtitles: What's the Difference?](https://www.ai-media.tv/knowledge-hub/insights/closed-captions-vs-subtitles/)

[vod-streaming-versus-live-streaming-versus-ott-the-modern-video-economy](https://cloudinary.com/guides/live-streaming-video/vod-streaming-versus-live-streaming-versus-ott-the-modern-video-economy)

[tv-advertising-explained](https://clearcode.cc/blog/tv-advertising-explained/)

[Awesome Video Github repo](https://github.com/krzemienski/awesome-video/)