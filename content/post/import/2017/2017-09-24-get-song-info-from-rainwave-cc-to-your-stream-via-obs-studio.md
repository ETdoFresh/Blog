---
title: Get Song Info from rainwave.cc to your stream via OBS Studio.
author: ETdoFresh
type: post
date: 2017-09-24T18:11:55+00:00
url: /get-song-info-from-rainwave-cc-to-your-stream-via-obs-studio/
linkedFacebookPostID:
  - 10102442561105218_10102437492487768
categories:
  - Programming

---
<span style="text-decoration: underline;">UPDATE 9/27/2017</span>  
Wow! Rainwave.cc tweeted me back with a much better solution. Hence the post below is for educational purposed. Use the much better (and much more official) link below. 🙂

<p style="text-align: center;">
  <a href="https://rainwave.cc/twitch/"><strong>https://rainwave.cc/twitch/</strong></a>
</p>

* * *

I love listening to video game remix music at <https://ocr.rainwave.cc>, and wanted a way I can show on my stream the information about the current song being played.

I&#8217;m sure there are probably easier ways to do this, but I made a small windows GUI Executable using C#/WPF that will download Album, Title, and Art from rainwave&#8217;s API, and I wanted to share it with you.[<img class="aligncenter size-medium wp-image-901" src="https://www.etdofresh.com/wp-content/uploads/2017/09/GetSongInfo-248x300.png" alt="" width="248" height="300" srcset="http://localhost/wp-content/uploads/2017/09/GetSongInfo-248x300.png 248w, http://localhost/wp-content/uploads/2017/09/GetSongInfo.png 346w" sizes="(max-width: 248px) 100vw, 248px" />][1]Download the project here:

  * Windows Binary: [SongInfo.zip][2] (232 KB)
  * Windows Source: [SongInfoSource.zip][3] (1085 KB)

This program will output files like Album.txt, Title.txt, Art.jpg that you can use in OBS as shown below.

[<img class="aligncenter size-large wp-image-905" src="https://www.etdofresh.com/wp-content/uploads/2017/09/GetSongStream-1024x555.png" alt="" width="840" height="455" srcset="http://localhost/wp-content/uploads/2017/09/GetSongStream-1024x555.png 1024w, http://localhost/wp-content/uploads/2017/09/GetSongStream-300x163.png 300w, http://localhost/wp-content/uploads/2017/09/GetSongStream-768x416.png 768w, http://localhost/wp-content/uploads/2017/09/GetSongStream-1200x650.png 1200w, http://localhost/wp-content/uploads/2017/09/GetSongStream.png 1920w" sizes="(max-width: 840px) 100vw, 840px" />][4]

 [1]: https://www.etdofresh.com/wp-content/uploads/2017/09/GetSongInfo.png
 [2]: https://www.etdofresh.com/wp-content/uploads/2017/09/SongInfo.zip
 [3]: https://www.etdofresh.com/wp-content/uploads/2017/09/SongInfoSource.zip
 [4]: https://www.etdofresh.com/wp-content/uploads/2017/09/GetSongStream.png