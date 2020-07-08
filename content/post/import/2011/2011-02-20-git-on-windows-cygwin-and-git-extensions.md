---
title: Git on Windows (Cygwin and Git Extensions)
author: ETdoFresh
type: post
date: 2011-02-21T01:14:00+00:00
url: /git-on-windows-cygwin-and-git-extensions/
blogger_blog:
  - etdofresh.blogspot.com
blogger_author:
  - ETdoFresh
blogger_permalink:
  - /2011/02/git-on-windows-cygwin-and-git.html
blogger_internal:
  - /feeds/8161366669954270448/posts/default/4436335911595092550
categories:
  - Uncategorized

---
Dear Blog,

<p style="text-align:center">
  <a href=""><img src="" /></a>
</p>

Setting up git (Version Control System) really did suck on Windows. It wasn&#8217;t a simple install this package, and all your problems are solved. I had major issues trying to use PuTTy, plink, and copSSH, which I believe most people use if they are using git on windows. I&#8217;m doing the cygwin approach. It&#8217;s soo much easier (to me at least). Setting up the server kind of sucks, but the client is easy. I&#8217;ll show how to setup the client today, and put up another post very shortly on how to setup a git server on windows using these exact same files.

# Step 1 &#8211; Download and install Cygwin

<p style="text-align:center">
  <a href=""><img src="" /></a>
</p>

Download cygwin from <http://www.cygwin.com/> ([Even Quicker Link][1])

  * Run **setup.exe**
  * Click **Next >**
  * Select **Install from Internet**. Click **Next >**
  * Keep Root Directory **C:cygwin**, and **Select All Users (RECOMMENDED)**. Click **Next >**
  * Personally, I change Local Package Directory to **C:cygwinpackages**. But wherever is fine.
  * Select **Direct Connection**, Click **Next >**
  * Select a mirror (I use http://mirror.cs.vt.edu), Click **Next >**
  * Should get a Setup Alert, Click **OK**
  * Select **All > Devel > git**. Select **All > Net > openssh**. Click **Next >**
  * Make sure Select required packages is checked, Click **Next >**
  * Let it download and install
  * Click **Finish**
  * Run it once. You should get a unix command prompt. Type in git<enter>, and you should see a list of options. Type in ssh<enter>, and you should also get a list of options.
  * If all looks alright, you are done with Cygwin (if you are just using this as a client)

# Step 2 &#8211; Download and install Git Extensions

<p style="text-align:center">
  <a href=""><img src="" /></a>
</p>

Download gitextensions MSI file from <http://code.google.com/p/gitextensions/> ([Even Quicker Link][2])

  * Run msi **installer**
  * Click **Next**
  * Verify path is OK for you. Click **Next**
  * Leave default options if you want, Click **Next**
  * Select **OpenSSH**, Click **Next**
  * Click **Install**
  * Let it install
  * Click **Finish**
  * Note: If you are prompted to install msysgit and kdiff3, just install kdiff3&#8230; otherwise download and install [kdiff3][3] (or whatever diff software you like)

# Step 3 &#8211; Setup Git Extensions

<p style="text-align:center">
  <a href=""><img src="" /></a>
</p>

  * Run Git Extensions
  * Select English (if you perfer) &#8211; The UK flag!
  * In settings (which should pop up right away) Select the Git tab 
      * Set command used to run git as **C:cygwinbingit.exe**
      * Set Path to linux tools as **C:cygwinbin**
  * Select Global settings 
      * Set perferred username and user email
  * Select Ssh 
      * Ensure **OpenSSH** is selected

# Step 4 &#8211; Use Git

<p style="text-align:center">
  <a href=""><img src="" /></a>
</p>

  * Click **Clone repository**
  * For Repository to clone, type in your **server** or directory (ie ssh://username@my.server.com/git/test.git)
  * Set Destination and subdirectory appropriately. Click **Clone**.
  * Log into your SSH server.
  * Click **OK** on success (I hope!)
  * Click **Yes** to view your repository.
  * You will only have to log into your SSH on every push (not for every commit)
  * Now get to work!

So, I know the issues I ran into using the putty, plink, msysgit may not be normal. But it definitely was a problem for me. So, here is my how-to on Cygwin and Git Extension, and I love this setup. I&#8217;ll get to that server how-to in the next couple of days. Later!

&#8211; ETdoFresh

 [1]: http://www.cygwin.com/setup.exe
 [2]: http://code.google.com/p/gitextensions/downloads/list
 [3]: http://kdiff3.sourceforge.net/