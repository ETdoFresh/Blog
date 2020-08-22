+++
author = "ETdoFresh"
date = 2020-08-22T21:34:36Z
excerpt = "In this article, we describe how to get your game server running at wss://your-dns-name.ext:port. We install and download a Let's Encrypt certificate on a server and put it in our Godot Project."
featured_image = "/uploads/2020/08/img_3705.jpg"
tags = ["Godot", "Multiplayer", "Websocket", "Linode", "DDNS", "PlatformBuddies"]
title = "How to Install a Godot Websocket SSL Game Server using Let's Encrypt Certificate"
url = ""

+++
In this article, we describe how to get your game server running at wss://your-dns-name.ext:port. We install and download a Let's Encrypt certificate on a server and put it in our Godot Project.

For this example we setup a barebones Linode Server with **Docker** and **git** \[Debian 9, Nanode 1GB: 1 CPU, 25GB Storage, 1GB RAM\].

## Setup a DNS/DDNS name

Let's Encrypt does not allow certificates to an IP Address. Hence, you need a DNS name. I used http://noip.com and pointed a DDNS name to my Linode IP address.

## Download Let's Encrypt

SSH into your Linode terminal and download Let's Encrypt from github.com

```bash
git clone https://github.com/letsencrypt/letsencrypt /opt/letsencrypt
```

## Install Let's Encrypt

Run the certificate downloader

```bash
cd /opt/letsencrypt/
./letsencrypt-auto certonly --standalone -d my_sweet_sweet_game.ddns.net
```

You should see something like this at the end...

> * Congratulations! Your certificate and chain have been saved at:
>   /etc/letsencrypt/live/my_sweet_sweet_game.ddns.net/fullchain.pem
>   Your key file has been saved at:
>   /etc/letsencrypt/live/my_sweet_sweet_game.ddns.net/privkey.pem
>   Your cert will expire on 2020-11-20. To obtain a new or tweaked
>   version of this certificate in the future, simply run
>   letsencrypt-auto again. To non-interactively renew _all_ of your
>   certificates, run "letsencrypt-auto renew"
> * Your account credentials have been saved in your Certbot
>   configuration directory at /etc/letsencrypt. You should make a
>   secure backup of this folder now. This configuration directory will
>   also contain certificates and private keys obtained by Certbot so
>   making regular backups of this folder is ideal.

## Download Certificates

Download cert.pem, chain.pem, and privkey.pem to your local machine.

_Note: If just using a SSH terminal, the files are copy/paste-able if you want to do the following and paste them to your local machine. Make SURE you have an new line after ---END BLAH BLAH---._

Local Windows Machine:

```bash
mkdir keys
cd keys
fsutil file createnew cert.pem 0
fsutil file createnew chain.pem 0
fsutil file createnew privkey.pem 0
```

Remote (Linode) Machine:

```bash
cat /etc/letsencrypt/live/my_sweet_sweet_game.ddns.net/cert.pem #copy and paste
cat /etc/letsencrypt/live/my_sweet_sweet_game.ddns.net/chain.pem #copy and paste
cat /etc/letsencrypt/live/my_sweet_sweet_game.ddns.net/privkey.pem #copy and paste
```

## Convert PEM to CRT/KEY files

So, we have the certificates locally now, but we need to convert them to a format Godot can use. Hence we'll need OpenSSL to convert these keys from PEM to CRT/KEY files.

```bash
openssl x509 -outform der -in cert.pem -out cert.crt
openssl x509 -outform der -in chain.pem -out chain.crt
openssl rsa -outform PEM -in privkey.pem -out privkey.key
```

## Copy CRT/KEY files to Godot Project

As mentioned above download the following files into your Godot Game Project. I recommend keeping these as private and secure as possible. (ie .gitignore commiting these files to your repo). Never let it leave your computer. etc etc

    copy (keys)/* path/to/GodotProject/keys/*

## Use keys on Godot's WebSocketServer.listen()

```python
server = WebSocketServer.new()
server.bind_ip = "*"
server.private_key = CryptoKey.new(); 
server.private_key.load("res://keys/privkey.key")
server.ssl_certificate = X509Certificate.new()
server.ssl_certificate.load("res://keys/cert.crt")
server.ca_chain = X509Certificate.new()
server.ca_chain.load("res://keys/chain.crt")
server.listen(port)
```

## The Rest...

Well, you know... make a game and use this server! :) Hope this helped! - ET