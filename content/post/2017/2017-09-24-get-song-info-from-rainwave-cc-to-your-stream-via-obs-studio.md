---
title: Get Song Info from rainwave.cc to your stream via OBS Studio.
author: ETdoFresh
type: post
date: 2017-09-24T18:11:55+00:00
url: /get-song-info-from-rainwave-cc-to-your-stream-via-obs-studio/
featured_image: /wp-content/uploads/2017/09/GetSongStream.png
hide_featured_image: true
linkedFacebookPostID:
  - 10102442561105218_10102437492487768
tags:
  - Utility
  - Twitch
  - Programming

---
__UPDATE 9/27/2017__  
Wow! Rainwave.cc tweeted me back with a much better solution. Hence the post below is for educational purposed. Use the much better (and much more official) link below. 🙂

<a href="https://rainwave.cc/twitch/"><strong>https://rainwave.cc/twitch/</strong></a>

---

I love listening to video game remix music at <https://ocr.rainwave.cc>, and wanted a way I can show on my stream the information about the current song being played.

I'm sure there are probably easier ways to do this, but I made a small windows GUI Executable using C#/WPF that will download Album, Title, and Art from rainwave's API, and I wanted to share it with you.

![](/wp-content/uploads/2017/09/GetSongInfo.png)

Download the project here:

  * Windows Binary: [SongInfo.zip][2] (232 KB)
  * Windows Source: [SongInfoSource.zip][3] (1085 KB)

This program will output files like Album.txt, Title.txt, Art.jpg that you can use in OBS as shown below.

![](/wp-content/uploads/2017/09/GetSongStream.png)

 [2]: https://www.etdofresh.com/wp-content/uploads/2017/09/SongInfo.zip
 [3]: https://www.etdofresh.com/wp-content/uploads/2017/09/SongInfoSource.zip