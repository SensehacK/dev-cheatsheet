## Youtube Dl

To Download video

> \$ youtube-dl https://www.youtube.com/watch?v=yVpbFMhOAwE

## Basic guide for better quality

Stack Exchange
You can download 1080p using youtube-dl, but you need to do a little extra work. Usually it will only download 720p as its max even if you can see 1080p on youtube.com.

Run with -F to see available formats:

> youtube-dl -F https://www.youtube.com/watch\?v\=-pxRXP3w-sQ

171         webm      audio only  DASH audio  115k , audio@128k (44100Hz), 2.59MiB (worst)
140         m4a       audio only  DASH audio  129k , audio@128k (44100Hz), 3.02MiB
141         m4a       audio only  DASH audio  255k , audio@256k (44100Hz), 5.99MiB
160         mp4       256x144     DASH video  111k , 12fps, video only, 2.56MiB
247         webm      1280x720    DASH video 1807k , 1fps, video only, 23.48MiB
136         mp4       1280x720    DASH video 2236k , 24fps, video only, 27.73MiB
248         webm      1920x1080   DASH video 3993k , 1fps, video only, 42.04MiB
137         mp4       1920x1080   DASH video 4141k , 24fps, video only, 60.28MiB
43          webm      640x360
18          mp4       640x360
22          mp4       1280x720    (best)

notice that youtube-dl has labeled the last option 1280x720 as the 'best' quality and that's what it will download by default, but that the line starting with 137 is actually higher quality 1920x1080. Youtube has separated the video and audio streams for the lines labeled DASH so we also need to pick the highest quality audio which in this case is the line starting with 141. Then we run youtube-dl again this time specifying the audio and video:

> youtube-dl -f 137+141 https://www.youtube.com/watch\?v\=-pxRXP3w-sQ

and it will download the 1080p video and auto-merge it with the highest-quality audio. It should also auto-deleted the separate downloaded parts. This method is a little extra work, but will get you the best results.

## Updating Youtube

Update Youtube-dl

> youtube-dl -U

Specific folder ownership
// User: defines just user
// $USER:$USER has user group also.
> sudo chown -R user: ~/.virtualenvs
> sudo chown $USER:$USER /usr/local/bin/youtube-dl
