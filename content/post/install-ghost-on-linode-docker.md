+++
author = "ETdoFresh"
date = 2020-07-05T22:23:24Z
excerpt = "Hi! Here are the steps I took to install Ghost on a Linode."
featured_image = "https://unsplash.com/photos/uWL3al1dom0/download"
tags = ["Ghost", "Docker", "Linode"]
title = "Install Ghost on Linode Docker"

+++
Hi! Here are the steps I took to install Ghost on a Linode.

Create a "Docker" Linode. Give it a few minutes to spin up.

Before I got started, I went ahead and made sure my domain was setup correctly in Linode.

![](/uploads/2020/07/image-20200705164204526.png)

And make sure your SOA Record and A/AAAA Record are accurate (and pointed to your Linode's IP Address)

![image-20200705164339060](https://etdofresh.com/content/images/2020/07/image-20200705164339060.png)

![image-20200705164432022](https://etdofresh.com/content/images/2020/07/image-20200705164432022.png)

Log into your Linode and create these folders where settings and persistent data should be stored.

    mkdir ~/content
    mkdir ~/mysql
    mkdir ~/nginx-conf
    mkdir ~/letsencrypt

Create \~/nginx-conf/default.conf \[Certbot will modify this for https\]

    server {
      listen 80;
      listen [::]:80;
      server_name etdofresh.com www.etdofresh.com;
      # Useful for Let's Encrypt
      location /.well-known/acme-challenge/ { root /usr/share/nginx/html; allow all; }
      location / {
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-Proto https;
        proxy_pass http://ghost:2368;
      }
    }

Create \~/docker-compose.yaml \[change etdofresh.com to your-domain.com\]

    version: '3'
    services:
    
      ghost:
        image: ghost:latest
        restart: always
        depends_on:
          - db
        environment:
          url: https://etdofresh.com
          database__client: mysql
          database__connection__host: db
          database__connection__user: root
          database__connection__password: your_database_root_password
          database__connection__database: ghost
        volumes:
          - ~/content:/var/lib/ghost/content
    
      db:
        image: mysql:5.7
        restart: always
        environment:
          MYSQL_ROOT_PASSWORD: your_database_root_password
        volumes:
          - ~/mysql:/var/lib/mysql
    
      nginx:
        image: nginx:latest
        restart: always
        depends_on:
          - ghost
        ports:
          - "80:80"
          - "443:443"
        volumes:
           - ~/letsencrypt:/etc/letsencrypt
           - ~/nginx-html:/usr/share/nginx/html
           - ~/nginx-conf:/etc/nginx/conf.d

Launch Docker-Compose

    docker-compose up -d

Open a bash into your nginx container

    docker ps ## Find NGINX_CONTAINER_ID [ie 6363edee96f6]
    docker exec -it NGINX_CONTAINER_ID /bin/bash

Now you should be inside your nginx container. Run Let's Encrypt certbot

    apt-get update
    apt-get install -y certbot python-certbot-nginx
    certbot --nginx

Here how I answered the prompts...

    Saving debug log to /var/log/letsencrypt/letsencrypt.log
    Plugins selected: Authenticator nginx, Installer nginx
    Enter email address (used for urgent renewal and security notices) (Enter 'c' to
    cancel): etdofresh@gmail.com
    
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    Please read the Terms of Service at
    https://letsencrypt.org/documents/LE-SA-v1.2-November-15-2017.pdf. You must
    agree in order to register with the ACME server at
    https://acme-v02.api.letsencrypt.org/directory
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    (A)gree/(C)ancel: A
    
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    Would you be willing to share your email address with the Electronic Frontier
    Foundation, a founding partner of the Let's Encrypt project and the non-profit
    organization that develops Certbot? We'd like to send you email about our work
    encrypting the web, EFF news, campaigns, and ways to support digital freedom.
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    (Y)es/(N)o: N
    
    Which names would you like to activate HTTPS for?
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    1: etdofresh.com
    2: www.etdofresh.com
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    Select the appropriate numbers separated by commas and/or spaces, or leave input
    blank to select all options shown (Enter 'c' to cancel): *blank*
    
    Obtaining a new certificate
    Performing the following challenges:
    http-01 challenge for etdofresh.com
    http-01 challenge for www.etdofresh.com
    2020/07/05 21:33:00 [notice] 1328#1328: signal process started
    Waiting for verification...
    Cleaning up challenges
    2020/07/05 21:33:04 [notice] 1330#1330: signal process started
    Deploying Certificate to VirtualHost /etc/nginx/conf.d/default.conf
    Deploying Certificate to VirtualHost /etc/nginx/conf.d/default.conf
    2020/07/05 21:33:07 [notice] 1332#1332: signal process started
    
    Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    1: No redirect - Make no further changes to the webserver configuration.
    2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
    new sites, or if you're confident your site works on HTTPS. You can undo this
    change by editing your web server's configuration.
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 2
    
    Redirecting all traffic on port 80 to ssl in /etc/nginx/conf.d/default.conf
    Redirecting all traffic on port 80 to ssl in /etc/nginx/conf.d/default.conf
    2020/07/05 21:33:24 [notice] 1334#1334: signal process started
    
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    Congratulations! You have successfully enabled https://etdofresh.com and
    https://www.etdofresh.com
    
    You should test your configuration at:
    https://www.ssllabs.com/ssltest/analyze.html?d=etdofresh.com
    https://www.ssllabs.com/ssltest/analyze.html?d=www.etdofresh.com
    - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
    
    IMPORTANT NOTES:
     - Congratulations! Your certificate and chain have been saved at:
       /etc/letsencrypt/live/etdofresh.com/fullchain.pem
       Your key file has been saved at:
       /etc/letsencrypt/live/etdofresh.com/privkey.pem
       Your cert will expire on 2020-10-03. To obtain a new or tweaked
       version of this certificate in the future, simply run certbot again
       with the "certonly" option. To non-interactively renew *all* of
       your certificates, run "certbot renew"
     - Your account credentials have been saved in your Certbot
       configuration directory at /etc/letsencrypt. You should make a
       secure backup of this folder now. This configuration directory will
       also contain certificates and private keys obtained by Certbot so
       making regular backups of this folder is ideal.
     - If you like Certbot, please consider supporting our work by:
    
       Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
       Donating to EFF:                    https://eff.org/donate-le

If all went smoothly, you should be able to go to your website's ghost config

    https://your-domain.com/ghost

**Just my idea.... I haven't tested this yet**

Create a bash script /etc/letsencrpy/renew-docker.sh. \[Don't forget to chmod +x renew-docker.sh\]

    apt-get update
    apt-get install -y certbot python-certbot-nginx
    certbot certonly -n --webroot -w /usr/share/nginx/html -d etdofresh.com --deploy-hook='service nginx restart'

Then we could schedule to run this on a scheduled time period

    sudo crontab -e

And adding line to run every day at 11PM (or whatever you like)

    0 23 * * *   /etc/letsencrpy/renew-docker.sh

## References

[https://www.linode.com/docs/websites/cms/ghost/how-to-install-ghost-cms-with-docker-compose-on-ubuntu-18-04/](https://www.linode.com/docs/websites/cms/ghost/how-to-install-ghost-cms-with-docker-compose-on-ubuntu-18-04/ "https://www.linode.com/docs/websites/cms/ghost/how-to-install-ghost-cms-with-docker-compose-on-ubuntu-18-04/")

[https://certbot.eff.org/lets-encrypt/debianstretch-nginx](https://certbot.eff.org/lets-encrypt/debianstretch-nginx "https://certbot.eff.org/lets-encrypt/debianstretch-nginx")