# Video Terms


## Text
### Subtitles

The term "subtitles" is used for transcriptions of spoken text providing translations in different languages for viewers.

**Subtitles** are a form of captioning used to translate the audio dialogue from one language into another. Simply put, subtitles translate a video’s language into another. You’ll see subtitles used in many foreign films and programs.

### Closed Captions

Closed captions are created to **allow people who are** **deaf or hard of hearing to experience the video**, so they also include background sounds and speaker changes. On the other hand, subtitles assume that the viewer can hear the audio and as a result do not contain the background sounds or notifications for speaker changes.

[What is 608 and 708 Closed Captioning?](https://www.3playmedia.com/blog/difference-cea-608-cea-708-captions/)


## Video

### Main Video


### SDR

### HDR

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


## Ads

### Pre Roll | Mid Roll | Post Roll

Pre roll just means ads that are played before content playback begins.
Mid Roll would be an ad being played in middle.
Post Roll ad at the end.

### Ad Break

An ad content which has duration of time to be played with resolution and links.


### Ad Schedule

Collection | Array of Ad Breaks in a video stream file.


## HLS 

Apple's implementation of delivering video content via internet HTTP Live Streaming format specification.
Android / Roku and other platforms use DASH instead of HLS.
This HLS file is also sometimes referred as manifest file.

`.m3u8` file format in Text readable format.

## [HLS Format Examples](HLS_types.md)

## VOD

Video on demand

Ads aren't valuable for first few days
C3 for VOD is not that valuable like Linear Live TV.

C3 
C4  - Day four


## Linear

Also referred as `TVE Linear`

[what is linear tv](https://target-video.com/what-is-linear-tv/)


## Live Asset


## T6 Title 6 

Basically just rules from USA govt. to make sure they comply with certain rules

[what-title-6-video](https://www.nexttv.com/news/what-title-6-video-381860)


## DAI - Dynamic Ad Insertion

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

### AV1




## Encoders

## Decoders




## SCTE 

Scete tag to find the information around HLS / stream.
Convey information 




## DVR


### CDVR

cloud DVR

[CDVR FAQs by Spectrum](https://www.spectrum.net/support/tv/cdvr-faq)

### Hot Recording 



## Upscaling 

### Soap Opera effect

Frame insertion / intermission / adding 
Interpolating
24 fps -> 60 fps


DSP (Digital Signal Processing)


## Analytics

### Nielson

The company to catch analytics by actual hardware in live tv.


## Reference

[Closed Captions vs Subtitles: What's the Difference?](https://www.ai-media.tv/knowledge-hub/insights/closed-captions-vs-subtitles/)


[vod-streaming-versus-live-streaming-versus-ott-the-modern-video-economy](https://cloudinary.com/guides/live-streaming-video/vod-streaming-versus-live-streaming-versus-ott-the-modern-video-economy)

[tv-advertising-explained](https://clearcode.cc/blog/tv-advertising-explained/)

[Awesome Video Github repo](https://github.com/krzemienski/awesome-video/)