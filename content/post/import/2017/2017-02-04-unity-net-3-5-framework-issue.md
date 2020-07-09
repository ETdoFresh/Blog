---
title: Unity .NET 3.5 Framework Issue
author: ETdoFresh
type: post
date: 2017-02-04T16:42:55+00:00
url: /unity-net-3-5-framework-issue/
featured_image: /wp-content/uploads/2017/02/62433-unity-capture.png
excerpt: I just wanted to write down my solution to an issue we were having at my university with getting .NET 3.5 framework installed.
tags:
  - Unity
  - Troubleshooting
  - Misc

---

I just wanted to write down my solution to an issue we were having at my university with getting .NET 3.5 framework installed.

## The Issue

When loading C# scripts from Unity into Visual Studio, we would get "The C# project "xxx" is targeting ".NETFramework, Version=v3.5,Profile=Unity Subset v3.5&#8243;, which is not installed on this machine". So obviously, we just install .NET 3.5 right?<!--more-->

## Next Issue

![](/wp-content/uploads/2017/02/0x800f081f.png)

We would then try to install .NET 3.5 and get this issue! I tried the following right afterwards.

  * Uninstall reinstall Visual Studio
  * Uninstall reinstall Unity

## The Solution

So the only thing that seemed to work for me is to actually get .NET 3.5 to install... hence I found this on a [Microsoft forum][3]:

  1. Delete the key: HKLM\Software\Policies\Microsoft\Windows\WindowsUpdate
  2. Open CMD as administrator
  3. net stop wuauserv
  4. net start wuauserv
  5. Download and install this: <https://www.microsoft.com/en-gb/download/details.aspx?id=21>

And that ended up working! Yay!

 [1]: http://www.etdofresh.com/wp-content/uploads/2017/02/62433-unity-capture.png
 [2]: http://www.etdofresh.com/wp-content/uploads/2017/02/0x800f081f.png
 [3]: https://answers.microsoft.com/en-us/windows/forum/windows_8-update/net-framework-35-fails-to-install-with-error-code/458928d0-57d4-42dc-8459-cfa61e107047