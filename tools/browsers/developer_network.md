
Usually with web you can easily inspect every resource being transfered back and forth. 
Irrespective of Google drive permissions you have for read/write/download.

When a use has given a read permission to the end user as long as you can access that device in its root or admin form you can easily decipher the encryption or DRM rules in place.
That could be a small script on top of the already defined script - with client side rendering or just inspect the original file in the Developer window.


## Access Google drive read only video

Sometimes you want to keep the video file on your machine - and the owner of that file has assigned some users certain permission of just read and not write. You can get granular as you want but what if you're hoping into an airplane and the 40 - 60mins video calls were being recorded before and you say to yourself. Neat I can utilize my travel time (in Airplane) to go over these videos and be upto date about it.
Not this fast - Enter DRM which will prevent you to download those files shared in a remote space. Now to watch that video - it will stream and what does streaming requires, constant internet access. But you don't want to pay for Airplane wifi.


You use Developer settings & network tab.


Instructions:

1.  Open the Inspect element. You can get this by using the keyboard shortcut Ctrl + Shift + I (on Mac: Option + Command + I)
2.  Inside the inspect element, Open the “Network” Tab.
3.  Search for “videoplayback” on the filter search. Make sure that you have selected “All” under the different file options available. If nothing shows up still, then reload the page and repeat the steps.
4. Right-click on any one of the search results and select “Open in new tab”.
	a.   Pro Tip💡: If you want to download the video with the highest resolution, then compare the sizes and download the one with the largest size.
5.  In the new tab with the video, Right-click again and select “Save Video As”.
6. Profit


## Download manager

Or you can use Rclone tool for easier downloading option. Haven't had any experience with it though.

## Reference

https://ourtechroom.com/tech/download-protected-view-only-files-google-drive/
https://codingcat.codes/2019/01/09/download-view-protected-pdf-google-drive-js-code/
https://www.reddit.com/r/Piracy/comments/tn3win/how_to_download_files_from_a_view_only_google/
https://github.com/kapitainsky/RcloneBrowser
https://www.digitbin.com/download-restricted-google-docs/