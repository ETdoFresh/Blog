---
title: Open with Unity Windows Context Menu
author: ETdoFresh
type: post
date: 2017-02-14T03:19:42+00:00
url: /open-with-unity-windows-context-menu/
categories:
  - Programming
tags:
  - Unity

---
[<img class="aligncenter size-medium wp-image-827" src="http://www.etdofresh.com/wp-content/uploads/2017/02/UnityContextWindow-300x193.png" alt="" width="300" height="193" srcset="http://localhost/wp-content/uploads/2017/02/UnityContextWindow-300x193.png 300w, http://localhost/wp-content/uploads/2017/02/UnityContextWindow.png 449w" sizes="(max-width: 300px) 100vw, 300px" />][1]I found this on Unity Forums (<https://forum.unity3d.com/threads/openwithunity-inf.325221/>). Thanks [rakkarage][2]!

  * Copy text into [OpenWithUnity.inf][3]
  * Right click on it
  * Click Install!

<pre class="lang:default decode:true " title="OpenWithUnity.inf">[version]
signature="$CHICAGO$"
 
[OpenWithUnityInstall]
CopyFiles = OpenWithUnity.Files.Inf
AddReg    = OpenWithUnity.Reg
 
[DefaultInstall]
CopyFiles = OpenWithUnity.Files.Inf
AddReg    = OpenWithUnity.Reg
 
[DefaultUnInstall]
DelFiles  = OpenWithUnity.Files.Inf
DelReg    = OpenWithUnity.Reg
 
[SourceDisksNames]
55="Open with Unity","",1
 
[SourceDisksFiles]
OpenWithUnity.INF=55
 
[DestinationDirs]
OpenWithUnity.Files.Inf = 17
 
[OpenWithUnity.Files.Inf]
OpenWithUnity.INF
 
[OpenWithUnity.Reg]
HKLM,%OWU%,DisplayName,,"%OpenWithUnityName%"
HKLM,%OWU%,UninstallString,,"rundll32.exe syssetup.dll,SetupInfObjectInstallAction DefaultUninstall 132 %17%\OpenWithUnity.inf"
HKCR,Directory\Shell\OpenWithUnity,,,"%OpenWithUnityAccel%"
HKCR,Directory\Shell\OpenWithUnity\command,,,"""C:\Program Files\Unity\Editor\Unity.exe"" -projectPath ""%1"""
HKCR,Directory\Shell\OpenWithUnity,Icon,,"C:\Program Files\Unity\Editor\Unity.exe"
 
[Strings]
OpenWithUnityName="OpenWithUnity PowerToy"
OpenWithUnityAccel="Open with &Unity"
OWU="Software\Microsoft\Windows\CurrentVersion\Uninstall\OpenWithUnity"</pre>

&nbsp;

 [1]: http://www.etdofresh.com/wp-content/uploads/2017/02/UnityContextWindow.png
 [2]: https://forum.unity3d.com/members/rakkarage.543898/
 [3]: http://www.etdofresh.com/wp-content/uploads/2017/02/OpenWithUnity.zip