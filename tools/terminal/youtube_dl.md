# YouTube

To Download video

> $ youtube-dl [https://www.youtube.com/watch?v=yVpbFMhOAwE](https://www.youtube.com/watch?v=yVpbFMhOAwE)

## Basic guide for better quality

Stack Exchange You can download 1080p using youtube-dl, but you need to do a little extra work. Usually it will only download 720p as its max even if you can see 1080p on youtube.com.

Run with -F to see available formats:

> youtube-dl -F [https://www.youtube.com/watch\?v\=-pxRXP3w-sQ](https://www.youtube.com/watch\?v\=-pxRXP3w-sQ)

171 webm audio only DASH audio 115k , audio@128k \(44100Hz\), 2.59MiB \(worst\) 140 m4a audio only DASH audio 129k , audio@128k \(44100Hz\), 3.02MiB 141 m4a audio only DASH audio 255k , audio@256k \(44100Hz\), 5.99MiB 160 mp4 256x144 DASH video 111k , 12fps, video only, 2.56MiB 247 webm 1280x720 DASH video 1807k , 1fps, video only, 23.48MiB 136 mp4 1280x720 DASH video 2236k , 24fps, video only, 27.73MiB 248 webm 1920x1080 DASH video 3993k , 1fps, video only, 42.04MiB 137 mp4 1920x1080 DASH video 4141k , 24fps, video only, 60.28MiB 43 webm 640x360 18 mp4 640x360 22 mp4 1280x720 \(best\)

notice that youtube-dl has labeled the last option 1280x720 as the 'best' quality and that's what it will download by default, but that the line starting with 137 is actually higher quality 1920x1080. YouTube has separated the video and audio streams for the lines labeled DASH so we also need to pick the highest quality audio which in this case is the line starting with 141. Then we run youtube-dl again this time specifying the audio and video:

> youtube-dl -f 137+141 [https://www.youtube.com/watch\?v\=-pxRXP3w-sQ](https://www.youtube.com/watch\?v\=-pxRXP3w-sQ)

and it will download the 1080p video and auto-merge it with the highest-quality audio. It should also auto-deleted the separate downloaded parts. This method is a little extra work, but will get you the best results.

## Updating YouTube

Update Youtube-dl

> youtube-dl -U

Specific folder ownership // User: defines just user // $USER:$USER has user group also.

> sudo chown -R user: ~/.virtualenvs sudo chown $USER:$USER /usr/local/bin/youtube-dl

## Playlist

If you hit any errors while downloading a big playlist, you can just ignore the errors and move forward with the execution. Use -i to ignore errors

> youtube-dl -i "[https://www.youtube.com/playlist?list=PLMBTl5yXyrGQ68Ny1mXCAaSwbjpcVwm49](https://www.youtube.com/playlist?list=PLMBTl5yXyrGQ68Ny1mXCAaSwbjpcVwm49)"

P.S “VideoGameDunkey’s Greatest hits url.

Start from certain number.

> youtube-dl --help, contains:

Video Selection: --playlist-start NUMBER Playlist video to start at \(default is 1\) --playlist-end NUMBER Playlist video to end at \(default is last\) --playlist-items ITEM\_SPEC Playlist video items to download. Specify indices of the videos in the playlist Thus, the option --playlist-start NUMBER should help you to start the playlist in the middle, specified by NUMBER.

[Source StackOverflow](https://stackoverflow.com/questions/44610370/how-to-use-youtube-dl-script-to-download-starting-from-some-index-in-a-playlist)

I have total 135 videos in my playlist. I have successfully downloaded 38 of them. So I manually used this command.

> youtube-dl --playlist-start 39 -u uname@gmail.com -p mypassword [https://www.udemy.com/learn-ethical-hacking-from-scratch/learn/v4/content](https://www.udemy.com/learn-ethical-hacking-from-scratch/learn/v4/content)

Its downloading my remaining 97 videos.

## Update

Use youtube-dlp as it's the latest fork for the updated youtube fixes.
[Youtube-DLP](https://github.com/yt-dlp/yt-dlp/)

## Alias

You can add this as an alias

> alias yt-dl='yt-dlp -f bestvideo+bestaudio'

Usage would be 
> yt-dl https://www.youtube.com/


## Private videos

If you want to download private signed in videos from a different source website behind a paywall.

First inpect the iFrame or embedded video with a right click, inspect - `This Frame` in Firefox or you choice of browser. Copy the unique web url to work with the command line tool to download it appropriately.

If it helps anyone else, this means it will look like this:

```
> youtube-dl --referer [https://your-original-website.tld](https://your-original-website.tld) [https://player.vimeo.com/video/](https://player.vimeo.com/video/)<id>

```

If you need to log into the original site to watch the video first, then use an [extension to export your Firefox cookie](https://addons.mozilla.org/en-US/firefox/addon/cookies-txt/) to a text file, then tell youtube-dl to use it:

```
`youtube-dl --cookies path/to/cookie.txt --referer https://your-original-website.tld https://player.vimeo.com/video/<id>`
```

https://www.reddit.com/r/youtubedl/comments/lbrb2y/downloading_embedded_vimeo_videos/


## Alfred Automation

Use Snippets feature to add one

Auto expansion :  allowed`  
Keyword = `:yd `
Type: Plain Text snippet - match destination

Snippet
```script
yt-dl "{clipboard}"
```
yt-dl has been mapped to `yt-dlp -f bestvideo+bestaudio` in my bash alias

## Note

I don't support downloading copyrighted videos, I just like to store them for educational purposes. Having them offline & readily available without any buffering or network constraints is really helpful in some circumstances like learning some skill off youtube while you're in airplane or at a remote location. Having your own playlists downloaded or synced locally could help you be productive without your reliance on internet.
Also as long as you are viewing any video in a web browser with appropriate DRM software installed. Even when watching videos you're essentially downloading them. So most of the service providers can't differentiate this on web. They can throttle the speed if you're querying too many network requests but I hardly find that is the case. Sometimes it will send you lots of fragmented data to make sure you're sending too many requests or make the UX little bit bad for people mining the website. Those are just preventive DOS attacks tools enforced by any Site reliability engineer or network engineer at different infrastructure networks. You may also get a Captcha or some kind of human intervention system. Google may try to serve you extra interruptions if you use `Firefox` or you aren't signed in the google account. It is their way of making sure bots aren't making tons of network requests.
It will always be a cat & mouse game and in order to understand underlying mechanisms you need to work from both perspectives.
Also for 99.50% they won't bother tinkering with their systems and User experience as they won't have the technical chops to follow through the article or research paper. So big companies won't fight too much for developers, engineers or technical users.
I can write quite a few articles on DRM and why it is bad in the overall space & creates a bad UX all around for people who want to access stuff legally. Remember everyone starts around with good side but they get tired and switch to Dark side `Anakin` Star Wars alter ego, **Darth Vader**

Good side: Kautilya Save
Dark side: SensehacK
