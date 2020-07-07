+++
author = "ETdoFresh"
date = 2020-07-05T06:17:00Z
excerpt = "So, i found out something cool today... when installing minio. I found out via these instructions I can forward a port directly to my local pc."
featured_image = "https://unsplash.com/photos/cKrpgejIZpU/download"
tags = ["Kubernetes"]
title = "Kubernetes open port to local machine"

+++
So, i found out something cool today... when installing minio

``` sh
helm install minio bitnami/minio
```

I found out via these instructions I can forward a port directly to my local pc.

``` sh
kubectl port-forward --namespace default svc/minio 9000:9000
Forwarding from 127.0.0.1:9000 -> 9000
Forwarding from [::1]:9000 -> 9000
```

In browser...

``` http
http://localhost:9000/minio
```

![](/uploads/2020/07/image-20200705011348639.png)

This is my local machine that i am administering from... I think this may open lots of cool opportunities for accessing the volumes inside...