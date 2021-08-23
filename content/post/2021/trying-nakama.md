---
title: Trying Nakama
author: ETdoFresh
date: 2021-08-11T00:00:00.000+00:00
excerpt: I was curious to see how Nakama played with Unity. Here are the steps I have done to try it out!
#url: "/trying-nakama/"
featured_image: /uploads/2021/08/nakama_graphic.svg
#hide_featured_image: true
tags:
- Network
- Nakama
- Unity
---

I was curious to see how Nakama played with Unity. Here are the steps I have done to try it out!

I'm following this guide:  
https://heroiclabs.com/docs/nakama/getting-started/docker-quickstart/

## **Download docker-compose.yml**

Download [docker-compose.yml](/uploads/2021/08/docker-compose.yml) into a *Local Nakama Directory*  
(i.e. C:\Nakama)

## **Run Docker Compose**

    cd {NakamaDirectory}
    docker compose up

## **Navigate to Console**

Just like that, the server is up! Noice!

Nakama Server located at: [http://localhost:7350](http://localhost:7350)  
Nakama Console located at: [http://localhost:7351](http://localhost:7351)  
*by default the username:password are admin:password*

## Checkout Documentation

So, after realizing it was super simple installing Nakama. I then started looking at some documents.

Unity Client Guide: https://heroiclabs.com/docs/nakama/client-libraries/unity-client-guide/  
Example Project: https://github.com/heroiclabs/unity-sampleproject

## Conclusion

Nakama is an awesome tool, and I will definitely use it in the future. However, I found that I had to get too much into the nitty gritty to get it working for simple games. Unreal Engine abstracts this away from me so I can focus on design. So, I think I'm going to continue using Unreal Engine for my current multiplayer projects. I need to make something fun before I decide to optimize. So, that's where I landed and that's where I'll continue.

