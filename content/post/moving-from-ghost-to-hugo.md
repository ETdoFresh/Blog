+++
author = "ETdoFresh"
date = 2020-07-06T10:13:50Z
description = "Moving from Ghost to Hugo"
feature_image = "/uploads/2020/07/54194774_10102925179519048_4139436063376539648_n.jpg"
title = "Moving from Ghost to Hugo"

+++
## Introduction

After 1 or 2 days, I realized slimming down from WordPress to Ghost was just the beginning. I was somewhat satisfied. However, after setting up comments and looking at other integrations for Ghost, I feel like I'm just using a mini/less functional WordPress. The markdown editing was the reason I made the switch, but then I realized, I might as well just scrap the database backend and keep all the files in a repo. I feel this way it is more manageable, and coder friendly.

So... here is my journey on switching to Hugo/GitHub...

## Install Hugo Locally

I followed [this guide](https://www.freecodecamp.org/news/your-first-hugo-blog-a-practical-guide/) for a nice quick start and getting a page up quickly.

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

While "hugo serve" is running, you can make changes to the markdown (.md) files, and you'll see the changes automatically refresh in the site. Neat.

## Getting Files onto your GitHub Repo

Here is how we get the files into the repo. (First make sure you create your repo in GitHub and get the link, ex https://github.com/ETdoFresh/Blog.git)

``` bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/ETdoFresh/Blog.git
git push --set-upstream origin master
```

At this point, we have the Hugo files on github.com, but we don't have an actual website yet.

## Setting up the GitHub Action

Every time we commit to the master branch, it'd be nice to have it automatically build and commit our website files to our github page. In order to do this, I've created a github action that should be able to do just this...

First, let's add secrets to our GitHub repo for GH_USERNAME and GH_TOKEN. You can add secrets in GitHub.com > Your Hugo Repo > Settings > Secrets

Next, create .github/workflows/main.yml

**Don't use this action... I realized I need to check into github/user/user.github.io**

``` yaml
name: Hugo Build to gh-pages
on:
  push:
    branches:
    - master
jobs:
  windows:
    name: Hugo Build
    runs-on: ubuntu-latest    
    steps:
    - uses: actions/checkout@v1
    - uses: ETdoFresh/Actions/HugoBuild@latest
    - uses: ETdoFresh/Actions/UploadToGithubPages@latest
      with:
          DIRECTORY_TO_UPLOAD: './public/'
          GITHUB_REPOSITORY: ETdoFresh/Blog
          GITHUB_USERNAME: ${{ secrets.GH_USERNAME }}
          GITHUB_TOKEN: ${{ secrets.GH_TOKEN }} 
```

_Note: Replace ETdoFresh/Blog with your repository_

Commit and Push Changes

``` bash
git add .
git commit -m "Add GitHub Action"
git push
```

If all went well, you now have a gh-pages branch. However, there's a chance we forgot to tell github to use this branch as a page. So in GitHub.com > Your Hugo Repo > Settings > Options > GitHub Pages