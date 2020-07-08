---
title: Corona Simulator shortcut
author: ETdoFresh
type: post
date: 2011-01-28T17:33:00+00:00
url: /corona-simulator-shortcut/
blogger_blog:
  - etdofresh.blogspot.com
blogger_author:
  - ETdoFresh
blogger_permalink:
  - /2011/01/corona-simulator-shortcut.html
blogger_internal:
  - /feeds/8161366669954270448/posts/default/3053815275536950184
categories:
  - Uncategorized

---
Dear Blog,

I decided that I am going to use Ansca Corona to develop a game I&#8217;m working on vs. Airplay SDK. This LUA language is soo much easier than C++. I still would love to have my games programmed in C++, but for just me, it&#8217;ll take too long to get to my final destination. So, LUA it is! Anyway, here is a quick batch file that I like to keep in my projects directory so all I have to do is drag the folder to this batch file, or type in the name of the porject I&#8217;m working on.

**simulate.cmd**

<pre>@echo off
echo -------------------------
echo Shortcut to LUA Simulator
echo -------------------------
echo.

SET coronaSimulator=%ProgramFiles(x86)%
IF "%coronaSimulator%" == "" SET coronaSimulator=%ProgramFiles%
SET coronaSimulator=%coronaSimulator%AnscaCorona SimulatorCorona 

Simulator.exe

IF NOT [%1] == [] GOTO PROCEED
SET /P simulateTarget=Enter name of your project? 

:PROCEED
IF NOT [%simulateTarget%] == [] SET simulateTarget="%simulateTarget%"
SET simulateTarget=%1%simulateTarget%main.lua

IF NOT EXIST %simulateTarget% GOTO MESSAGE
start "Corona Simulator" "%coronaSimulator%" %simulateTarget%
GOTO END

:MESSAGE
echo Project does not exist: %simulateTarget%
pause

:END
</pre>