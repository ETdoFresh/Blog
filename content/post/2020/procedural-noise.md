---
title: Procedural Noise
author: ETdoFresh
type: post
date: 2020-03-15T00:00:00Z
excerpt: Here is the start of my journey into understanding Procedural Content Generation. First I'm testing out some procedural noise.
url: /procedural-noise/
featured_image: /uploads/2020/03/image-20200710135930349.png
hide_featured_image: true
tags:
  - PCG
  - Research
  - UNO
  - Game
  - Unity
---

{{< unity "https://www.etdofresh.com/ProceduralNoise" >}}

Here is the start of my journey into understanding Procedural Content Generation. First I'm testing out some procedural noise.

https://github.com/ETdoFresh/ProceduralNoise {{< sub Source Code >}}

## Pseudo Random Noise

{{< image src="/uploads/2020/03/image-20200710140338675.png" >}}

A computer cannot generate what is considered purely random noise. It is based on some other factors like time, algorithms, etc. However, to us humans, it seems random enough. Here what random noise looks like on a grid of pixels where 0 is black and 1 is white. we generate a pseudo random number between 0.0 and 1.0.

## Perlin Noise

{{< image src="/uploads/2020/03/image-20200710135930349.png" >}}

As show above, there is no relationship between one pixel to the next. Ken Perlin introduced an algorithm for computer graphics that would use random generation but also include spatial relationships between pixels.

## Quick Demo

{{< image src="/uploads/2020/03/image-20200710140605334.png" >}}

Here is a REALLY rough demo of using Perlin Noise to generate a grass and forest top down map. Feel free to try it out using the link above.