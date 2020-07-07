+++
author = "ETdoFresh"
date = 2020-07-05T06:21:00Z
excerpt = "I forgot this, and then found it out again. Figured I'd just write a small memory fragment here... To monitor/watch a Kubernetes object..."
featured_image = "https://unsplash.com/photos/dBI_My696Rk/download"
tags = ["Kubernetes"]
title = "Monitoring Kubernetes Pods/Services/etc"

+++
I forgot this, and then found it out again. Figured I'd just write a small memory fragment here...

To monitor/watch a Kubernetes object...

``` bash
kubectl get pod -w

NAME                                   READY   STATUS    RESTARTS   AGE
etdofresh-wordpress-7d8ff94558-zfbfl   1/1     Running   0          10h
etdofresh-wordpress-mariadb-0          1/1     Running   0          12h
ghost-test2-669b4b469-gxw66            1/1     Running   0          5h43m
ghost-test2-mariadb-0                  1/1     Running   0          5h46m
minio-688b86c7c4-qzglp                 1/1     Running   0          4m38s
```

And basically it just writes a new line if something happens.