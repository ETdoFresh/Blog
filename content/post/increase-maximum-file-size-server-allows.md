+++
author = "ETdoFresh"
author-image = ""
date = 2020-07-05T05:00:00Z
description = ""
feature_image = "/uploads/2020/07/untitled.png"
tags = []
title = "Increase Maximum File Size Server Allows"

+++
When setting up a blog server, as we did in [Install Ghost on Linode Docker](https://etdofresh.com/install-ghost-on-linode-docker/), you may have realized that sometimes the server does not like huge files. In order to up the maximum file size allowed, edit your \~/nginx-conf/default.conf

```bash
server {
    ...
    client_max_body_size 500M;
}
```

Then restart your, in this site's case

```bash
docker exec -it $DOCKER_POD_ID service nginx restart
```

### References

[https://etdofresh.com/install-ghost-on-linode-docker/](https://etdofresh.com/install-ghost-on-linode-docker/ "https://etdofresh.com/install-ghost-on-linode-docker/")

[https://www.tecmint.com/limit-file-upload-size-in-nginx/](https://www.tecmint.com/limit-file-upload-size-in-nginx/ "https://www.tecmint.com/limit-file-upload-size-in-nginx/")