+++
author = "ETdoFresh"
date = 2020-07-04T22:57:00Z
excerpt = ""
featured_image = "https://unsplash.com/photos/lRoX0shwjUQ/download"
tags = ["Linode", "Kubernetes"]
title = "Move Wordpress Site from Linode to LKE"

+++
Right now, I have a wordpress site being hosted on a single Linode server. However, I'm making the jump to kubernete services/Linode Kubernetes Engine (LKE). Here is my devops journey to getting this done.

## My Current Setup

![image-20200704164142351](image-20200704164142351.png)

* Linode Server running Debian 8 with 1 CPU, 30GB Storage, and 2GB RAM \[$10/mo\]
  * Nginx installed
  * Php installed
  * Wordpress downloaded
  * Nginx, Php configuration files updated to work with wordpress
  * Hosting Port 80/443 for wordpress site
  * Hosting Port 22 for ssh
  * All maintenance to server done via ssh terminal like ssh.exe or putty.exe

## Goal of new setup

My personal motivation for doing this is to have a cluster setup that can serve whatever services I want. Let's say I want to serve my wordpress site, game server 1, and game server 2, and another website. This may be able to run on 1 server... or maybe 2 servers. However many servers it takes can be abstracted away with kubernetes. I say "run service", and kubernetes just places these services onto available servers. If we notice there is too much CPU usage on our cluster, we can add more servers at a click of a button.

## Start a Cluster

![](/uploads/2020/07/image-20200704165438984.png)

In Kubernetes first we add a cluster server which will maintain all nodes (worker servers) \[$10/mo\]

![](/uploads/2020/07/image-20200704165851970.png)

Then we add nodes into node pools. Here we have just 1 node in our node pool \[$10\]. Now we are done purchasing our servers! Now we can start adding services... but first, let's get setup to do some command line administration...

## What are Docker, Kubernetes, Helm, etc

So, I'm not an expert, just a user... and in my head, this is what each is:

* Docker - A container that holds all software and dependencies. Hence a docker container on my computer runs exactly the same as a docker container on your computer. It is meant to be reset and rebuilt, hence within the container itself, it should never hold any persistent data.
* Kubernetes - A docker orchestration platform. Kubernetes is a cluster of servers that is managed my a master node. Administrators like you and me tell the node to "add or remove" service \[which is a set of steps of how to deploy docker containers\], and it manages how the docker containers are deployed among your cluster.
* Helm - Kubernetes has many parts. Pods, Deployments, Services, Persistent Volumes, etc. Each of these can have one or more files needed to get a single service up and running. Helm charts is a way to gather all these files into one place and specify your particular needs without having to dive into many files.

## Installing software

I'm on Windows 10, but I assume these steps are quite similar on other machines. So I'm not going to go in deep detail, but here is the order in which i did this.

1. Install [Docker Desktop](https://www.docker.com/products/docker-desktop)
   * This should enable docker.exe to be run in your command prompt
2. Install [Kubernetes command-line tool](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
   * I think now docker now comes with kubectl.exe
   * Make sure it's in your PATH environment variables
3. Install [Helm](https://helm.sh/docs/intro/install/)

Once you have these 3 pieces of software, you should be ready to start administering your Kubernetes cluster.

## Configuring kubectl to communicate to LKE Cluster

If you try running kubectl after installation it will probably try to hit localhost. So we need to redirect it to LKE cluster. There are probably other ways to do this, but I simply replaced my default config file with my linode config file.

* Download {YourClusterName}-kubeconfig.yaml as shown in the Start a Cluster section of this site
* Locate your .kube\\config. Mine was located in c:\\users\\etgarcia\\.kube\\config
* Rename .kube\\config to .kube\\config.bak \[to relive the old days\]
* Move {YourClusterName}-kubeconfig.yaml to .kube/config

Test it out by typing

``` sh
kubectl get nodes
```

You should see the servers you reserved

``` sh
kubectl get nodes
NAME                        STATUS   ROLES    AGE   VERSION
lke3699-4883-5eff748a56fe   Ready    <none>   28h   v1.17.3
```

## Setup Persistent Volumes

As I probably mentioned above, Docker containers are mortal. They should not hold data that needs to live. So, in order to keep any kind of data that needs to survive an outage, we need to add it to a persistent volume. So, I did this via Kubernetes. Here's some background as I understand it...

* Persistent Volumes - The actual storage volume of data. It can be NFS. Some local path on server. Or, in our case, a Linode Block Storage \[10GB $1/mo\]
* Persistent Volume Claim - an abstraction of Persistent Volume. We don't care how we have space at this point, as long as we have X space to do something

So, assuming kubectl is properly setup as we did in the section before, I first wrote up this simple yaml to claim some space on Linode...

``` yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: etdofresh-wordpress-db-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
---
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: etdofresh-wordpress-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
```

Then we go ahead and claim some space!

``` sh
kubectl apply -f create_new_pvc.yaml
persistentvolumeclaim/etdofresh-wordpress-db-pvc created
persistentvolumeclaim/etdofresh-wordpress-pvc created
```

We now have claimed 2 volumes on Linode Volumes that should be automatically generated for us. So if we checkout Linode...

![](/uploads/2020/07/image-20200704174207357.png)

I don't know how to reclaim the links to persistent volumes if you accidentally delete them using kubectl delete. So, if you want to be extra protective of your persistent volume, save the following text somewhere safe:

```sh
kubectl get pv -o yaml
```

## Going straight to the Helm

Well, there is so much to learn between docker and kubernetes, it's crazy. But, you know what!? Let's jump straight to the helm chart and get this wordpress site working!

For this install, we are going to use bitnami/wordpress installation. It's pretty straight forward (if you don't peek behind the curtains :p) To do, we first add the repo so we can easily install wordpress with one command...
\[Instructions also found [here](https://github.com/bitnami/charts/tree/master/bitnami/wordpress)\]

    helm repo add bitnami https://charts.bitnami.com/bitnami

But hold on, let's get our custom values correct...

``` yaml
wordpressUsername: etdofresh
wordpressPassword: my_password
wordpressEmail: etdofresh@gmail.com
wordpressFirstName: ET
wordpressLastName: Garcia
wordpressBlogName: ETdoFresh
wordpressTablePrefix: wp_

resources:
  limits: {}
  requests:
    memory: 512Mi
    cpu: 300m

service:
  type: LoadBalancer
  port: 80
  httpsPort: 443
  httpsTargetPort: https
  metricsPort: 9117
  nodePorts:
    http: ""
    https: ""
    metrics: ""
  externalTrafficPolicy: Cluster
  annotations: {}
  loadBalancerSourceRanges: []

persistence:
  enabled: true
  existingClaim: etdofresh-wordpress-pvc
  accessMode: ReadWriteOnce
  size: 10Gi

mariadb:
  enabled: true
  replication:
    enabled: false
  db:
    name: etdofresh_wordpress
    user: etdofresh
    password: my_wordpress_db_password

  rootUser:
    password: my_wordpress_db_root_password

  master:
    persistence:
      enabled: true
      existingClaim: etdofresh-wordpress-db-pvc
      accessModes:
        - ReadWriteOnce
      size: 10Gi

externalDatabase:
  host: localhost
  user: etdofresh
  password: ""
  database: etdofresh_wordpress
  port: 3306
```

So, there are a lot of settings here. The thing to note is that these are the values we want to override (or at least potentially override) from default installation. So here are the highlights from above:

* WordPress site information is stored here
* We could leave password blank and bitnami generate one for us, but if we ever rebuild this helm, the password is then stored on the persistent volume and potentially lost forever, so figured a hard coded \[insecurely placed in this file\] would work
* Persistent volume claims use "existingClaim"s that we made earlier

With our settings in place, now we can install this helm!

``` sh
helm install --values=values.yaml etdofresh-wordpress bitnami/wordpress
```

This creates a new helm instance called etdofresh-wordpress.

```sh
helm ls
NAME                    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
etdofresh-wordpress     default         1               2020-07-04 12:38:37.871794 -0500 CDT    deployed        wordpress-9.3.17        5.4.2
```

## Done... for now....

Well, that's it. We now have a WordPress running in kubernetes using persistent volume.