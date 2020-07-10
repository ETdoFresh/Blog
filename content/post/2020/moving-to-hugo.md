+++
title = "Moving to Hugo"
date = 2020-07-07T06:38:06Z
author = "ETdoFresh"
excerpt = "Oh man. I've been putting so many hours trying to figure out how to move my blog over to Hugo/GitHub."
featured_image = "https://unsplash.com/photos/L7jHvobH6-g/download"
tags = ["Hugo", "WordPress", "Ghost", "Blog Setup"]

+++
Oh man. I've been putting so many hours trying to figure out how to move my blog over to Hugo/GitHub. I'm getting very close. I found a tool, [WordPress to Hugo Exporter](https://github.com/SchumacherFM/wordpress-to-hugo-exporter), which will hopefully get me going. I copied my WordPress site locally ([here's how](/copy-wordpress-manually/)), and now I'm running the export from WordPress to Hugo...

```bash
/var/www/html/wp-content/plugins/wordpress-to-hugo-exporter#
mkdir tmp
php hugo-export-cli.php ./tmp
```

It just finished! Nice! Well, all my blog posts are now here... I think? Now I just have to spend hours formatting them. :p

Well once it's done, they should in GitHub and hosted free! Nice!

Alright! It's 3AM now... I'm crazy... good night!