## Introduction

After 1 or 2 days, I realized slimming down from WordPress to Ghost was just the beginning. I was somewhat satisfied, but after setting up comments and looking at other integrations, I feel like I'm just using a mini/less functional WordPress when using Ghost. The markdown editing was the reason I made the switch, but then I realized, I might as well just scrap the database backend and keep all the files in a repo.

I am in GitHub everyday, so it only makes sense that I make my posts in here as well.

So... here is my journey on switching to Hugo/GitHub...

## Install Hugo Locally

I followed this guide for a nice quick start and getting a page up quickly.

``` bash
choco install hugo
hugo new site ETdoFresh
```

Download a theme. For example, download [ghostwriter](https://github.com/jbub/ghostwriter/archive/master.zip) and unzip into ETdoFresh/themes/ghostwriter.

Copy examplepages to content

``` bash
cd ETdoFresh
xcopy themes\ghostwriter\exampleSite\content\post\ content\post\
xcopy themes\ghostwriter\exampleSite\content\page\ content\page\
```

Now you can test the site by running

``` bash
hugo serve
```

And going to

``` http
http://localhost:1313/
```

While "hugo serve" is running, you can make changes to the markdown (.md) files, and you'll see the changes live on the site.