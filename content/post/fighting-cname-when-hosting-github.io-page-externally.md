+++
author = "ETdoFresh"
date = 2020-07-07T16:42:36Z
excerpt = ""
featured_image = "/uploads/2020/07/untitled2.png"
tags = ["GitHub", "Hugo"]
title = "Fighting CNAME when Hosting GitHub.io Page Externally"

+++
One of the problems I found when auto-deploying my blog to my GitHub.io account is that after I commit, I see "404 There isn't a GitHub Pages site here."

To fix it, I'd then go back to GitHub.com > GitHub.io Repository > Settings > Custom Domain and repair my missing domain name...

![](/uploads/2020/07/capture.PNG)

Then looking at the commits, I realize, I have been deleting CNAME from the root each time my script auto-deployed the website!

So, to fix that, I simply added CNAME to the root of my static folder, and now my website seems to work after commits.

Hope that helps!