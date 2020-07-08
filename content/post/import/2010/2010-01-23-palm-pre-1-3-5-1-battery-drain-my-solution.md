---
title: Palm Pre 1.3.5.1 Battery Drain – My Solution
author: ETdoFresh
type: post
date: 2010-01-23T19:56:00+00:00
url: /palm-pre-1-3-5-1-battery-drain-my-solution/
blogger_blog:
  - etdofresh.blogspot.com
blogger_author:
  - ETdoFresh
blogger_permalink:
  - /2010/01/palm-pre-1351-battery-drain-my-solution.html
blogger_internal:
  - /feeds/8161366669954270448/posts/default/6406993823058122945
categories:
  - Uncategorized

---
Dear Blog,

I figure I&#8217;d blog about my struggles with Palm Pre battery issues after certain updates!

<p align="center">
  <a href="http://lh4.ggpht.com/_yEPuIWl8ybE/S1tUg5GJDdI/AAAAAAAABBU/ph8GUdqW_Mo/s1600/IMG_8021.jpg"><img src="http://lh4.ggpht.com/_yEPuIWl8ybE/S1tUg5GJDdI/AAAAAAAABBU/ph8GUdqW_Mo/s288/IMG_8021.jpg" width="225" /></a>
</p>

**Where I&#8217;m Starting Off**

I bought a Palm Pre, flashed a custom firmware on it (qinray 1.0.4 v2). I then used novaterm to install Dropbear which is a SSH server for my phone so that I can just PuTTy and sFTP right into it. Then I setup ez-ipudate so that I could have a static hostname for my dynamic-IP address, so I only had to type myhostname.homeip.net instead of 123.45.54.32. All convenient, and never really had an issue. My phone would last me about 2 days without a charge.

**Before 1.3.5.1 &#8211; Updating PRL**

The first time I encounter phone dying within one day problem with little or no usage was right around the 1.3 update. The solution I found to this was updating the PRL and disabling roaming. In weak signal areas, your phone keeps polling the area and draining your battery fast! Especially if you have roaming on (that&#8217;s a whole bunch of more places to poll).

<p align="center">
  <a href="http://lh6.ggpht.com/_yEPuIWl8ybE/S1thVzk3SaI/AAAAAAAABBY/qJ6s6YXDl7A/s1600/Image3.jpg"><img src="http://lh6.ggpht.com/_yEPuIWl8ybE/S1thVzk3SaI/AAAAAAAABBY/qJ6s6YXDl7A/s144/Image3.jpg" width="115" height="144" /></a><a href="http://lh3.ggpht.com/_yEPuIWl8ybE/S1thVwRgCxI/AAAAAAAABBc/WTGIhhCvopg/s1600/Image4.jpg"><img src="http://lh3.ggpht.com/_yEPuIWl8ybE/S1thVwRgCxI/AAAAAAAABBc/WTGIhhCvopg/s144/Image4.jpg" width="115" height="144" /></a><a href="http://lh4.ggpht.com/_yEPuIWl8ybE/S1thWEpsSAI/AAAAAAAABBg/HK7fwokrBSs/s1600/Img_8032.jpg"><img src="http://lh4.ggpht.com/_yEPuIWl8ybE/S1thWEpsSAI/AAAAAAAABBg/HK7fwokrBSs/s144/Img_8032.jpg" width="103" height="144" /></a>
</p>

So first easiest thing to try is disabling your roaming, which can be done right from your phone. Press your menu button on bottom of your phone, tap the phone icon, click your provider on top left of screen (most likely Sprint), tap Preferences, Drag down to the Network Section, Tap Voice Network, Select Sprint Only.

While you&#8217;re there also try updating your PRL (Preferred Roaming List). It&#8217; just a button almost at the dead bottom of the previous step.

If you can&#8217;t update your PRL from your phone (like me), use computer software to update your PRL&#8230; I won&#8217;t go into detail here, but overall: I find the latest PRL on the net (60659 during this post) and use QPST&#8217;s Service Programming -> Roam Tab -> Browse for my PRL and click Write to Phone. Done!

**The 1.3.5.1 Update**

Well I have lots of homebrew software as stated in my _Where I&#8217;m Starting_ off section. I can&#8217;t really tell you which step fixed my problem, but here goes my story. After about a week or two of charging my phone every night because battery dies within 1 day, I got fed up. This weekend, I was determined to find out what was wrong. But before that, I could not even turn on my phone with the A/C adapter plugged in! So I pop the battery out, wait about a minute, pop it back in, and it starts charging! Nice! But I was determined to find out what was wrong.

I read some forums online, and I noticed people without homebrew had significantly more post praising the battery life, where homebrewers like me were shunning the battery. So immediately I thought, it must be my homebrew software. At this point, I have an SSH, sFTP, and DynDNS on my phone. My focus immediately went to DynDNS. How often was it polling? I had no clue. So I added _period=86400_ to _/opt/etc/ez-ipupdate.conf_ to poll just once a day. This could have fixed my problem, but I delved deeper.

<p align="center">
  <a href="http://www.webos-internals.org/images/3/36/Preware_ss1.png"><img src="http://www.webos-internals.org/images/3/36/Preware_ss1.png" height="144" /></a>
</p>

I then read this [post][1], and installed Preware. I love Preware! I was doing everything by SSH before, but little did I know, this could be my last SSH session ever! I agreed to everything, and installed a few apps, like battery mointor, flashlight, etc. More imporantly, Preware didn&#8217;t register I had software like Dropbear (SSH), and EZ-IPUpdate installed, so I just reinstalled them on top of my previous installs from Preware. Left the battery monitor software on over night last night. Woke up, and had only a 1.52% drop of battery per hour vs something like 8% &#8211; 10%. Oh man! It was wonderful!

Oh, and I use GMAIL, Exchange, Wifi, and EVDO (email polls every 30 minutes).

**Conclusion**

I&#8217;m excited about my new battery life, and maybe it&#8217;s not Palm&#8217;s fault entirely, but maybe us tweakers may be to blame (just little itty bitty bit). But once Palm learns to leave tweaker&#8217;s settings alone, I think we can live in harmony! 🙂 Later!

&#8211; ETdoFresh

PS &#8211; Use [WebOS Internals][2] for all your Homebrew needs! Very cool place!

 [1]: http://www.webos-internals.org/wiki/Application:Preware
 [2]: http://www.webos-internals.org/wiki/Main_Page