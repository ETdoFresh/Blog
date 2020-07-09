---
title: Setting up a torrent
author: ETdoFresh
type: post
date: 2010-05-10T04:50:00+00:00
url: /setting-up-a-torrent/
blogger_blog:
  - etdofresh.blogspot.com
blogger_author:
  - ETdoFresh
blogger_permalink:
  - /2010/05/setting-up-torrent.html
blogger_internal:
  - /feeds/8161366669954270448/posts/default/1175957196543883117
categories:
  - Uncategorized

---
<div xmlns='http://www.w3.org/1999/xhtml'>
  <p>
    Here's a quick, no frills, text-only tutorial on setting up your own torrent (and personal tracker), for family photos, family movies, etc (using uTorrent)...
  </p>
  
  <ol>
    <li>
      Get your external IP address (or dyndns address)
    </li>
    <li>
      Get your uTorrent listening port (by Options > Speed Guide)
    </li>
    <li>
      Forward that port on router (sorry non-tech savvy peepz)
    </li>
    <li>
      Enable Tracker (Options > Preferences > Advanced > bt.enable.tracker = true)
    </li>
    <li>
      Create Torrent! <ol>
        <li>
          File > Create New Torrent...
        </li>
        <li>
          Select files you want to server
        </li>
        <li>
          Trackers = http://yourExternalIP:yourForwardedPort/announce
        </li>
        <li>
          Check Start Seedings and Private Torrent
        </li>
        <li>
          Click Create and Save As... to make torrent file (then wait)
        </li>
        <li>
          If you see the torrent in your list, a green arrow, and everything is seeding, you are doing swell! If not, check your port and check it with the built-in Speed test in Options > Speed Guide
        </li>
      </ol>
    </li>
    
    <li>
      Give that torrent to all your friends and ensure tracker is always up (because of private torrent option).
    </li>
  </ol>
  
  <p>
    Good luck all, and to all a good night!
  </p>
  
  <p>
    – E.T.
  </p>
</div>