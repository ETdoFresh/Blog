+++
author = "ETdoFresh"
date = 2020-07-05T06:59:00Z
excerpt = ""
featured_image = "https://unsplash.com/photos/uJmaoWQ64YY/download"
tags = ["Kubernetes"]
title = "Connecting to Kubernetes Dashboard"

+++
First install updated dashboard

``` sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
```

Then start the dashboard

``` sh
kubectl proxy
```

And finally, use a browser to open up the dashboard

``` http
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
```

I just use the kubeconfig file in my ~/.kube/config directory (or c:\users\my_username\\.kube\config)