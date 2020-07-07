---
title: Symbolic Link Batch File
author: ETdoFresh
type: post
date: 2010-12-20T05:26:00+00:00
url: /symbolic-link-batch-file/
blogger_blog:
  - etdofresh.blogspot.com
blogger_author:
  - ETdoFresh
blogger_permalink:
  - /2010/12/symbolic-link-batch-file.html
blogger_internal:
  - /feeds/8161366669954270448/posts/default/7833074565034271449
categories:
  - Uncategorized

---
Dear Blog,

I use Boxee, and when I download DVDs, they don&#8217;t show up as episodes on my TV Guide. Someone suggested making symbolic links&#8230; Sounds good to me. Here&#8217;s a batch file I use to generate these symbolic links (not catching me renaming 100&#8217;s of files

<pre>@echo off
SETLOCAL EnableDelayedExpansion
echo -------------------------------------------------------------------------
echo  This will make symbolic links for your ISO/IMG files
echo -------------------------------------------------------------------------
echo.

IF "%~f1" == "" (
  echo No file dragged onto this script
  pause
  EXIT
)

SET /P season=Season (ie 1)? 
SET /P episodeStart=Starting Episode (ie 1)? 
SET /P episodeEnd=Ending Episode (ie 4)?

IF NOT DEFINED season SET season=1
IF NOT DEFINED episodeStart SET episodeStart=1
IF NOT DEFINED episodeEnd SET episodeEnd=4

IF %season% LSS 10 SET season=0%season%
IF %episodeStart% LSS 10 SET episodeStartZero=0%episodeStart%

SET firstEpisode=%~n1 S%season%E%episodeStartZero%%~x1
MOVE "%~dpf1" "%~dp1%firstEpisode%"

IF %episodeStart% GEQ %episodeEnd% EXIT
SET /A episodeStart=episodeStart + 1

FOR /l %%n IN (%episodeStart%,1,%episodeEnd%) DO (
  SET currentEpisode=%%n
  IF !currentEpisode! LSS 10 SET currentEpisode=0!currentEpisode!
  mklink "%~dpn1 S%season%E!currentEpisode!%~x1" "%firstEpisode%"
)
pause</pre>

_Edit:_ Hmm, my sickbeard renames the files, so here is my newer method&#8230; I append each dvd with their first episode, like first dvd would now end in s01e01. Do that for each dvd. Then sickbeard renames it. To show up nicely in boxee, I run the following, slighltly modified script:

<pre>@echo off
SETLOCAL EnableDelayedExpansion
echo -------------------------------------------------------------------------
echo  This will make symbolic links for your ISO/IMG files
echo -------------------------------------------------------------------------
echo.

IF "%~f1" == "" (
  echo No file dragged onto this script
  pause
  EXIT
)

SET /P season=Season (ie 1)? 
SET /P episodeStart=Starting Episode (ie 2)? 
SET /P episodeEnd=Ending Episode (ie 4)?

IF NOT DEFINED season SET season=1
IF NOT DEFINED episodeStart SET episodeStart=2
IF NOT DEFINED episodeEnd SET episodeEnd=4

IF %season% LSS 10 SET season=0%season%

FOR /l %%n IN (%episodeStart%,1,%episodeEnd%) DO (
  SET currentEpisode=%%n
  IF !currentEpisode! LSS 10 SET currentEpisode=0!currentEpisode!
  mklink "%~dp1S%season%E!currentEpisode!%~x1" "%~f1"
)
pause
</pre>