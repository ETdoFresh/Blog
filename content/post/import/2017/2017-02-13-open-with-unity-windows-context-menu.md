---
title: Open with Unity Windows Context Menu
author: ETdoFresh
type: post
date: 2017-02-14T03:19:42+00:00
url: /open-with-unity-windows-context-menu/
featured_image: /wp-content/uploads/2017/02/UnityContextWindow.png
tags:
  - Unity
  - Utility
  - Windows
  - Programming

---

  * Copy text into [OpenWithUnity.inf][3]
  * Right click on it
  * Click Install!

```ini
[version]
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
OWU="Software\Microsoft\Windows\CurrentVersion\Uninstall\OpenWithUnity"
```

### Reference

https://forum.unity3d.com/members/rakkarage.543898/

 [3]: http://www.etdofresh.com/wp-content/uploads/2017/02/OpenWithUnity.zip