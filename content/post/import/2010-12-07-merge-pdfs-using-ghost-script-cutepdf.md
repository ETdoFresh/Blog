---
title: Merge PDFs using Ghost Script (CutePDF)
author: ETdoFresh
type: post
date: 2010-12-07T18:02:00+00:00
url: /merge-pdfs-using-ghost-script-cutepdf/
blogger_blog:
  - etdofresh.blogspot.com
blogger_author:
  - ETdoFresh
blogger_permalink:
  - /2010/12/merge-pdfs-using-ghost-script-cutepdf.html
blogger_internal:
  - /feeds/8161366669954270448/posts/default/6653334542702405121
categories:
  - Uncategorized

---
Dear Blog,

Here is a batch file (.cmd or .bat) to merge PDFs

<pre>@echo off
echo -------------------------------------------------------------------------
echo  This will merge all your pdfs in the current directory to an output.pdf
echo -------------------------------------------------------------------------
echo.
Setlocal EnableDelayedExpansion
%~d0
cd %~p0
set /p MERGEFILE=Output file (no need to add .pdf)? 
set PDFMERGE=
for %%f in (*.pdf) do set PDFMERGE=!PDFMERGE! "%%f"
"C:Program FilesGPLGSgswin32c" -sDEVICE=pdfwrite -dNOPAUSE -dQUIET -dBATCH -sOutputFile="%MERGEFILE%.pdf" %PDFMERGE%
pause</pre>