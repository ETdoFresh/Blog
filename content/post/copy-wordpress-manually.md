+++
author = "ETdoFresh"
date = 2020-07-07T06:25:15Z
excerpt = ""
featured_image = "https://unsplash.com/photos/hzdgFPz1V24/download"
tags = []
title = "Copy WordPress Manually"

+++
First, I think it'd be best to copy our wordpress site over to our local computer...

Copy over files from your server... you probably just need the wp-contents folder

Dump your wordpress database and download. To dump your SQL...

```bash
mysqldump --databases wordpress > wordpress.sql
```

Setup a local instance of wordpress with docker-compose. Create a new folder called *wordpress*. Create *wordpress/www* folder and add *wordpress/docker-compose.yml*

```yaml
version: "3"
services:
  db:
    image: mysql:5.7
    restart: always
    volumes:
      - db_data:/var/www/mysql
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    networks:
      - wp

  wordpress:
    depends_on:
      - db
    image: wordpress
    restart: always
    volumes: ["./www/:/var/www/html"]
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
    ports:
      - 80:80
      - 443:443
    networks:
      - wp

  phpmyadmin:
    depends_on:
      - db
    image: phpmyadmin/phpmyadmin
    restart: always
    ports:
      - 8080:80
    environment:
      PMA_HOST: db
      MYSQL_ROOT_PASSWORD: password
    networks:
      - wp

networks:
  wp:
  
volumes:
  db_data:
```

Copy your *wordpress.sql* into *wordpress/*. Get the mysql containter id and copy wordpress.sql into container.

```bash
docker ps
docker cp wordpress.sql CONTAINER_ID:/wordpress.sql
```

Go into container and copy data into database

```bash
docker exec -it CONTAINER_ID /bin/bash
mysql -u DB_USERNAME -p < wordpress.sql
```

I'll be honest. I've been through this process a few times. Here is tweak you'll probably have to make...

- Navigate to http://localhost:8080 *phpmyadmin*
- Change *wordpress.wp_options.home* from http://SOME-ADDRESS to http://localhost
- Change *wordpress.wp_options.siteurl* from http://SOME-ADDRESS to http://localhost

A tweak I had to go through that you probably shouldn't... I had a custom named 10-year old database (wordpress_etdofresh). The way I did this was create a vanilla wordpress with wordpress as the database. I went through the setup and populated the wordpress data with all new data. I then logged into WordPress and went to an admin page (like the posts page). I then went to phpmyadmin, renamed db wordpress to wordpress_2 and renamed wordpress_etdofresh to wordpress.

Then copy your site's wp-content into *wordpress/www*. If you go to localhost, your site should be there. Now modify, backup, or do whatever you need to do! Good luck! - ET
