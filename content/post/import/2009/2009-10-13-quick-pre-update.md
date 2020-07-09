---
title: Quick Pre Update
author: ETdoFresh
type: post
date: 2009-10-13T07:52:00+00:00
url: /quick-pre-update/
blogger_blog:
  - etdofresh.blogspot.com
blogger_author:
  - ETdoFresh
blogger_permalink:
  - /2009/10/quick-pre-update.html
blogger_internal:
  - /feeds/8161366669954270448/posts/default/3031014805956489651
categories:
  - Uncategorized

---
Dear Blog,

Just wanted to post a quick Pre Update. I found a solution to get My Tether 1.5 to work with Palm Pre WebOS 1.2.1. I used the method from [Leathal's Post on precentral.net][1]. Here's a quick copy and past of his method:

1) Connect your Pre in dev mode to your computer  
2) [Download the old driver][2]  
3) Open up WebOS Quick Install and choose "Send File" from the Tools menu  
4) Browse to where you saved sd8xxx.ko  
5) Paste the following line in Destination Folder:  
/lib/modules/2.6.24-palm-joplin-3430/kernel/net/wifi/  
6) Click Send to Device and reboot your Pre when it's done (Sym+Orange+R)

Cool! Also you can edit the SSID in the sh file found in TetherService.jar found in /usr/lib/luna/java. Happy PalmPre'ing!

&#8211; E.T.

 [1]: http://forums.precentral.net/web-os-development/208788-howto-reenable-wifi-tethering-free-mytether.html
 [2]: http://www.mediafire.com/file/jywhtmrymzl/sd8xxx.ko