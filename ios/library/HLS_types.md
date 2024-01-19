# HLS Playlist Types

## VOD

Video on Demand (VOD)
Representing the entire duration of the stream | video asset.
This allows the client full access to the entire video asset fragments.

[apple dev | vod doc](https://developer.apple.com/documentation/http-live-streaming/video-on-demand-playlist-construction)

the `EXT-X-PLAYLIST-TYPE` tag with a value of `VOD`

```ts
#EXT-X-PLAYLIST-TYPE:VOD

#EXT-X-ENDLIST
```

## Linear | Live

Live Playlist (sliding window)

[apple dev doc](https://developer.apple.com/documentation/http-live-streaming/live-playlist-sliding-window-construction)

It doesn't have `EXT-X-PLAYLIST-TYPE` and `EXT-X-ENDLIST` in the HLS file.

```ts
#EXT-X-TARGETDURATION:10
#EXT-X-VERSION:4
#EXT-X-MEDIA-SEQUENCE:1
```

## Event Playlist

the `EXT-X-PLAYLIST-TYPE` tag with a value of `EVENT`

[apple dev doc](https://developer.apple.com/documentation/http-live-streaming/event-playlist-construction)

Event playlists are typically used when you want to allow the user to seek to any point in the event, such as for a concert or sports event.

It doesn't have `EXT-X-ENDLIST` in the initial HLS file.
```ts
#EXT-X-PLAYLIST-TYPE:EVENT
#EXTINF:10.0,
fileSequence0.ts
.
..
...
#EXTINF:10.0,
fileSequence4.ts
```

It doesn’t initially have an `EXT-X-ENDLIST` tag, indicating that new media files will be added to the playlist as they become available.

```ts
#EXT-X-PLAYLIST-TYPE:EVENT
#EXTINF:10.0,
fileSequence65.ts

#EXTINF:10.0,
fileSequence69.ts
#EXT-X-ENDLIST
```

## Multi Variant

[Apple dev | Multi variant doc](https://developer.apple.com/documentation/http-live-streaming/creating-a-multivariant-playlist)

It doesn't have EXT-X-PLAYLIST-TYPE in the .m3u8 ? playlist file.

```ts
#EXT-X-STREAM-INF:BANDWIDTH=150000,RESOLUTION=416x234,CODECS="avc1.42e00a,mp4a.40.2"
http://example.com/low/index.m3u8

#EXT-X-STREAM-INF:BANDWIDTH=640000,RESOLUTION=640x360,CODECS="avc1.42e00a,mp4a.40.2"
http://example.com/high/index.m3u8)

```

