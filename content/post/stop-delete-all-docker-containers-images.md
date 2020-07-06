+++
author = "ETdoFresh"
date = 2020-07-05T22:16:28Z
draft = true
excerpt = "Sometimes it's useful to start with a clean slate and remove all Docker containers and even images. Here are some handy shortcuts."
featured_image = "https://unsplash.com/photos/eyJhcHBfaWQiOjExNzczfQ/download"
tags = []
title = "Stop/Delete All Docker Containers/Images"

+++
Sometimes it's useful to start with a clean slate and remove all Docker containers and even images. Here are some handy shortcuts.

## **List all containers (only IDs)**

    docker ps -aq

## **Stop all running containers**

    docker stop $(docker ps -aq)

## **Remove all containers**

    docker rm $(docker ps -aq)

## **Remove all images**

    docker rmi $(docker images -q)

**Copied from:**

[https://blog.baudson.de/blog/stop-and-remove-all-docker-containers-and-images](https://blog.baudson.de/blog/stop-and-remove-all-docker-containers-and-images "https://blog.baudson.de/blog/stop-and-remove-all-docker-containers-and-images")