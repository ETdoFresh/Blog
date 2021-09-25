---
title: AHK TrayTip for Windows Virtual Desktop Name
author: ETdoFresh
date: 2021-09-24T00:00:00.000+00:00
excerpt: A quick how-to on setting up a tray tip that shows Windows Desktop Name when switching desktops
#url: "/url"
featured_image: "/uploads/2021/09/Screenshot 2021-09-24 233822.png"
hide_featured_image: false
tags:
- Windows
- Virtual Desktop

---

When using keyboard shortcuts to switch virtual desktops in Windows (Windows 10), it'd be nice to know which desktop you are on, *especially if you named them!*

## Shortcut Keys

| Keyboard Shortcut              | Action                           |
| ------------------------------ | -------------------------------- |
| {Win} + {Tab}                  | Desktop Manager (1)              |
| {Ctrl} + {Win} + {Left Arrow}  | Previous Virtual Desktop         |
| {Ctrl} + {Win} + {Right Arrow} | Next Virtual Desktop             |
| {Ctrl} + {Win} + D             | New Virtual Desktop              |
| {Ctrl} + {Win} + F4            | Close/Delete Virtual Desktop (2) |

*(1) Rename your desktops in Desktop Manager*  
*(2) Your existing windows will get moved to another virtual desktop upon closing*

{{< figure src="/uploads/2021/09/Screenshot 2021-09-24 235900.png" title="Windows 10 Desktop Manager" >}}

## AHK TrayTip Script

I sometimes like to use AutoHotKey (AHK) to create simple scripts to make my life easier. In all fairness, after a while, I tend to delete them... but when I have that itch, this scratches!

Alas, here's the script to show TrayTip on your current desktop. I even contributed a good amount to this script! 😋

You can also download the script and icon here... [virtualdesktoptraytip.zip](/uploads/2021/09/virtualdesktoptraytip.zip) [2.15 KB]

```ahk
; Display Virtual Desktop Name as AHK TrayTip by ETdoFresh

IconName = virtualdesktoptraytip.ico
IfExist, %IconName%
    Menu, Tray, Icon, %IconName%

^#Left::
    global CurrentDesktop, CurrentDesktopName
    Send ^#{Left}
    sleep 500
    mapDesktopsFromRegistry()
    readCurrentDesktopNameFromRegistry()
    TrayTip Desktop %CurrentDesktop%, %CurrentDesktopName%, 1, 0x11
    return

^#Right::
    global CurrentDesktop, CurrentDesktopName
    Send ^#{Right}
    sleep 500
    mapDesktopsFromRegistry()
    readCurrentDesktopNameFromRegistry()
    TrayTip Desktop %CurrentDesktop%, %CurrentDesktopName%, 1, 0x11
    return

readCurrentDesktopNameFromRegistry() {
    global CurrentDesktop, CurrentDesktopId, CurrentDesktopName
    s := CurrentDesktopId
    FolderName := "{"
    FolderName := FolderName SubStr(s, 7, 2) SubStr(s, 5, 2) SubStr(s, 3, 2) SubStr(s, 1, 2)
    FolderName := FolderName "-"
    FolderName := FolderName SubStr(s, 11, 2) SubStr(s, 9, 2)
    FolderName := FolderName "-"
    FolderName := FolderName SubStr(s, 15, 2) SubStr(s, 13, 2)
    FolderName := FolderName "-"
    FolderName := FolderName SubStr(s, 17, 4)
    FolderName := FolderName "-"
    FolderName := FolderName SubStr(s, 21, 12)
    FolderName := FolderName "}"
    RegRead, CurrentDesktopName, HKEY_CURRENT_USER, SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\VirtualDesktops\Desktops\%FolderName%, Name
    if (CurrentDesktopName = "") {
        CurrentDesktopName = Desktop %CurrentDesktop%
    }
}

; I found the following functions at:
; https://www.computerhope.com/tips/tip224.htm
mapDesktopsFromRegistry() {
    global CurrentDesktop, DesktopCount, CurrentDesktopId
    ; Get the current desktop UUID. Length should be 32 always, but there's no guarantee this couldn't change in a later Windows release so we check.
    IdLength := 32
    SessionId := getSessionId()
    if (SessionId) {
        RegRead, CurrentDesktopId, HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\SessionInfo\%SessionId%\VirtualDesktops, CurrentVirtualDesktop
        if (CurrentDesktopId) {
            IdLength := StrLen(CurrentDesktopId)
        }
    }
    ; Get a list of the UUIDs for all virtual desktops on the system
    RegRead, DesktopList, HKEY_CURRENT_USER, SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\VirtualDesktops, VirtualDesktopIDs
    if (DesktopList) {
        DesktopListLength := StrLen(DesktopList)
        ; Figure out how many virtual desktops there are
        DesktopCount := DesktopListLength / IdLength
    }
    else {
        DesktopCount := 1
    }
    ; Parse the REG_DATA string that stores the array of UUID's for virtual desktops in the registry.
    i := 0
    while (CurrentDesktopId and i < DesktopCount) {
        StartPos := (i * IdLength) + 1
        DesktopIter := SubStr(DesktopList, StartPos, IdLength)
        OutputDebug, The iterator is pointing at %DesktopIter% and count is %i%.
        ; Break out if we find a match in the list. If we didn't find anything, keep the
        ; old guess and pray we're still correct :-D.
        if (DesktopIter = CurrentDesktopId) {
            CurrentDesktop := i + 1
            OutputDebug, Current desktop number is %CurrentDesktop% with an ID of %DesktopIter%.
            break
        }
        i++
    }
}


getSessionId()
{
    ProcessId := DllCall("GetCurrentProcessId", "UInt")
    if ErrorLevel {
        OutputDebug, Error getting current process id: %ErrorLevel%
        return
    }
    OutputDebug, Current Process Id: %ProcessId%
    DllCall("ProcessIdToSessionId", "UInt", ProcessId, "UInt*", SessionId)
    if ErrorLevel {
        OutputDebug, Error getting session id: %ErrorLevel%
        return
    }
    OutputDebug, Current Session Id: %SessionId%
    return SessionId
}
```

