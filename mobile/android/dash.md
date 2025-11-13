
## Intro

** AI Generated **

Dynamic Adaptive Streaming over HTTP (DASH) is a standardized protocol that provides smooth video streaming over the internet by breaking video into segments and delivering them via HTTP, allowing the video player to dynamically switch between different quality levels in real-time to match the viewer's available bandwidth and network conditions. This adaptive approach ensures a buffer-free experience, leverages existing HTTP infrastructure, and is supported by numerous streaming platforms and devices. 


How DASH Works

1. Segmentation: Video content is divided into small, time-aligned segments. [[1](https://docs.momentohq.com/media-storage/performance/adaptive-bitrates/dash), [5](https://bitmovin.com/blog/dynamic-adaptive-streaming-http-mpeg-dash/)]
2. Multiple Bitrates: Each segment is encoded into multiple versions at different quality levels and bitrates. [[1](https://docs.momentohq.com/media-storage/performance/adaptive-bitrates/dash), [5](https://bitmovin.com/blog/dynamic-adaptive-streaming-http-mpeg-dash/)]
3. Media Presentation Description (MPD): A manifest file, the MPD, describes the available segments, their quality levels, and their locations on the server. [[5](https://bitmovin.com/blog/dynamic-adaptive-streaming-http-mpeg-dash/), [6](https://www.mpeg.org/standards/MPEG-DASH/), [7](https://www.cdnetworks.com/glossary/dash-protocol/#:~:text=How%20DASH%20Works%20DASH%20streaming%20divides%20media,based%20on%20network%20conditions%20and%20device%20capabilities.), [8](https://resi.io/glossary/adaptive-bitrate-streaming/#:~:text=Before%20streaming%20begins%2C%20the%20video%20player%20downloads,HLS%20protocol%20uses%20a%20.%20m3u8%20playlist.), [9](https://dl.acm.org/doi/pdf/10.1145/3458306.3460997#:~:text=Each%20segment%20is%20encoded%20into%20several%20different,within%20the%20Media%20Presen%2D%20tation%20Description%20\(MPD\).), [10](https://www.sciencedirect.com/science/article/abs/pii/S2452414X21000406#:~:text=MPD%20is%20a%20manifest%20file%20that%20contains,spatial%20and%20temporal%20resolutions%20of%20available%20representations.)]
4. HTTP Delivery: Segments are delivered to the client device using the standard HTTP protocol, which is compatible with most networks and firewalls. [[2](https://www.qualcomm.com/media/documents/files/qualcomm-research-dynamic-adaptive-streaming-over-http-dash.pdf), [4](https://www.cloudflare.com/learning/video/what-is-mpeg-dash/)]
5. Adaptive Bitrate Switching: The player continuously monitors network conditions and, based on the MPD, requests the appropriate quality segment to ensure a seamless and high-quality playback experience. [[1](https://docs.momentohq.com/media-storage/performance/adaptive-bitrates/dash), [2](https://www.qualcomm.com/media/documents/files/qualcomm-research-dynamic-adaptive-streaming-over-http-dash.pdf), [11](https://ricki-lee.medium.com/understanding-dash-a-comprehensive-guide-to-adaptive-bitrate-streaming-5f9dc63be5f9#:~:text=Whether%20you're%20streaming%20on%2Ddemand%20content%20or%20live,playback%20across%20diverse%20devices%20and%20network%20conditions.)]

Key Advantages

- Smooth Playback: Real-time adaptation to network changes prevents buffering. [[1](https://docs.momentohq.com/media-storage/performance/adaptive-bitrates/dash)]
- Standardization: MPEG-DASH is an international ISO/IEC standard, ensuring broad interoperability. [[2](https://www.qualcomm.com/media/documents/files/qualcomm-research-dynamic-adaptive-streaming-over-http-dash.pdf), [12](https://en.wikipedia.org/wiki/Dynamic_Adaptive_Streaming_over_HTTP)]
- HTTP Infrastructure: Uses existing web servers, CDNs, and caches, making it cost-effective and scalable. [[2](https://www.qualcomm.com/media/documents/files/qualcomm-research-dynamic-adaptive-streaming-over-http-dash.pdf), [13](https://www.wowza.com/blog/mpeg-dash-dynamic-adaptive-streaming-over-http)]
- Wide Support: Compatible with major streaming platforms, devices (Smart TVs, mobile phones), and web browsers. [[3](https://getstream.io/glossary/mpeg-dash-streaming/), [14](https://corp.kaltura.com/blog/mpeg-dash/)]
- Flexibility: Supports both live and on-demand streaming and can be used with various media formats. [[5](https://bitmovin.com/blog/dynamic-adaptive-streaming-http-mpeg-dash/), [6](https://www.mpeg.org/standards/MPEG-DASH/)]

Common Uses

- Video-on-Demand (VOD): Delivering movies and TV shows. [[6](https://www.mpeg.org/standards/MPEG-DASH/), [15](https://ieeexplore.ieee.org/iel7/6287639/9312710/09422745.pdf#:~:text=Traditional%20video%20sources%20such%20as%20video%2Don%2Ddemand%20\(i.e.%2C,Adaptive%20Streaming%20Over%20HTTP%20\)%20\)%20%5B2%5D.)]
- Live Streaming: Broadcasting events and other live content. [[5](https://bitmovin.com/blog/dynamic-adaptive-streaming-http-mpeg-dash/), [6](https://www.mpeg.org/standards/MPEG-DASH/), [16](https://d1.awsstatic.com/whitepapers/amazon-cloudfront-for-media.pdf#:~:text=live%20events%2C%20such%20as%20sport%2C%20concerts%2C%20news%2C,using%20one%20or%20more%20different%20streaming%20technologies.), [17](https://dev.to/binoy123/revolutionizing-content-delivery-an-introduction-to-video-encoding-and-ott-streaming-53gf#:~:text=Live%20streaming%20enables%20the%20broadcasting%20of%20events%2C,like%20HLS%20or%20DASH%20for%20live%20streaming.)]
- Cross-Platform Content Delivery: Providing a consistent streaming experience across different devices and networks. [[1](https://docs.momentohq.com/media-storage/performance/adaptive-bitrates/dash), [11](https://ricki-lee.medium.com/understanding-dash-a-comprehensive-guide-to-adaptive-bitrate-streaming-5f9dc63be5f9#:~:text=Whether%20you're%20streaming%20on%2Ddemand%20content%20or%20live,playback%20across%20diverse%20devices%20and%20network%20conditions.)]


Common Uses

- Video-on-Demand (VOD): Delivering movies and TV shows. 

- Live Streaming: Broadcasting events and other live content. 

- Cross-Platform Content Delivery: Providing a consistent streaming experience across different devices and networks.


## Apple Swift equivalent

[HLS](HLS.md)


