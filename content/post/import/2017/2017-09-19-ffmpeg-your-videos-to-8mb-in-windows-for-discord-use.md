---
title: FFMPEG Your Videos to 8MB in Windows for Discord Use
author: ETdoFresh
type: post
date: 2017-09-20T03:15:45+00:00
url: /ffmpeg-your-videos-to-8mb-in-windows-for-discord-use/
categories:
  - Programming

---
Here's a little windows batch script for sharing your "idea" or "thought" videos that are perhaps too big for Discord. I use FFMPEG to reencode the video to under the 8MB limit.

<pre class="lang:default decode:true" title="2DiscordVideo.cmd">@echo off
cd /D %~p0
SET output=%~n1_8MB.mp4
SET /P seconds=How many seconds is the video? 
SET /A "totalBitrate=64000/seconds"
SET overheadBitrate=100
SET audioBitrate=96
SET /A "videoBitrate=totalBitrate-audioBitrate-overheadBitrate"
ffmpeg -y -i %1 -c:v libx264 -b:v %videoBitrate%k -pass 1 -b:a %audioBitrate%k -f mp4 NUL && \
ffmpeg -i %1 -c:v libx264 -b:v %videoBitrate%k -pass 2 -b:a %audioBitrate%k "%output%"
del /q ffmpeg2pass-*.log ffmpeg2pass-*.mbtree
pause</pre>

I've packaged this code and ffmpeg.exe together for easy distribution later.

[Download 2DiscordVideo][1] [15.5MB]

**Instructions**: Drag YOUR.VIDEO onto 2DiscordVideo.cmd. Type in how many seconds your video is. It should then perform a 2 pass encoding of your video that will hopefully be less that 8MB. It will be located in the same directory as ffmpeg.exe and be named YOUR_8MB.VIDEO.

Good luck!

 [1]: https://www.etdofresh.com/wp-content/uploads/2017/09/2DiscordVideo.zip